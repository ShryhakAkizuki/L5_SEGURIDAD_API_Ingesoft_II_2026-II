8 # Laboratorio 5 - Seguridad en APIs

Entrega del Laboratorio 5 del curso **Ingeniería de software II** (2026-II).

## Integrantes

| # | Nombre |
|---|--------|
| 1 | Oscar Leonardo Riveros Perez |
| 2 | Jader Camilo Rodriguez Arboleda |
| 3 | Juan Luis Arteaga Mantovani |
| 4 | Daniel Oñate Hernandez |

## Requirements

* Maven
* Gson
* Spring Boot Web

## Server

To run the server, run the project inside ejercicio3. It is necessary to generatew the certificate. You can do so using the following command

```Bash
keytool -genkeypair -alias seii -keyalg RSA -keysize 2048 -validity 30 \
-storetype PKCS12 -keystore src/main/resources/keystore.p12 \
-dname "CN=localhost" -ext "SAN=dns:localhost,ip:127.0.0.1"
```
Running it generates `keystore.p12`. It asks for a password, store it safely, and create an environmental variable with it using one of the following commands

#### PowerShell
```PowerShell
$env:KEYSTORE_PASSWORD = "your_actual_key"
``` 

#### Linux 
```Bash
export KEYSTORE_PASSWORD="your_actual_key"
```

Then run 

``` Shell
keytool -exportcert -alias seii -keystore src/main/resources/keystore.p12 -rfc -file seii.crt
```
That command generates `seii.crt`.

## Client

For the client, it is necessary to import the previously created `seii.crt`. to do so, use the following command

```Shell
keytool -importcert -alias seii -file seii.crt -keystore confianza.p12 -storetype PKCS12 -noprompt
```

Then store the certificate using 

``` Shell
java -Djavax.net.ssl.trustStore=confianza.p12   -Djavax.net.ssl.trustStorePassword="contrasena"   
-cp target/classes:target/dependency/*  com.ejercicio3d.demo.Main
```

In our case, to properly run the client, it was necessary for the dependencies to be stored meaning to compile it, we used 

```Shell
./mvnw compile dependency:copy-dependencies
```



