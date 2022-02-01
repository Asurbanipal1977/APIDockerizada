### PROBLEMAS CON CLIENTEDNS
- Se para el clienteDNS puesto que usa el 100% de la CPU en caso contrario. Para solucionar este problema había que instalar la
versión 21h2 y la extensión KB5005611. Esta es la url para instalarlo:
https://mega.nz/file/pN4hnY7B#Zxw2LDQCeQKv-rr4wmOaJ-Mx16AXWnrY3c82C7Gi4uk

Se instala con este comando:
DISM /Online /Add-Package /PackagePath:"D:\Descargas\Windows10.0-KB5005611-x64.cab"

- Para desactivar el servicio:
reg add "HKLM\System\CurrentControlSet\Services\Dnscache" /v "Start" /t REG_DWORD /d "4" /f
- Para activarlo de nuevo:
reg add "HKLM\System\CurrentControlSet\Services\Dnscache" /v "Start" /t REG_DWORD /d "2" /f

Ahora ya funciona y no hace falta pararlo.


### DOCKER PARA WINDOWS
- Para arrancar un docker de prueba:
docker run -dp 82:80 docker/getting-started

 docker build -t docker101tutorial .
 docker run -d -p 82:80 --name docker-tutorial docker101tutorial

 docker ps -> contenedores en ejecución
 docker ps -a -> Estado del contenedor

 docker run -it ubuntu bash -> Permite ejecutar la imagen de ubuntu en un bash

### DOCKERIZAR APLICACIÓN .NET CORE
 Para dockerizar una aplicación .net core:
 - https://docs.docker.com/samples/dotnetcore/
 - https://www.youtube.com/watch?v=RY5gJyjQMdw -> video explicativo

 1. Se crea el proyecto.
 2. Se crea el fichero Dockerfile y .dockerignore
 3. Se construye mediante el comando: docker build .
 4. Ejecutamos docker build . desde la powershell
 5. Se hace docker images y se encuentra el id de la imagen. En este caso de prueba era: dfc2884809b7
 6. Se expone en el puerto 83, por ejemplo: docker run -dp 83:80 dfc2884809b7
 7. Con docker container ls veremos que se ejecuta ese contenedor.
 8. Se ejecuta http://localhost:83/weatherforecast

Para subirlo a docker HUB:
1. docker tag 48f7f1955a02 asurbanipal1977/apidockerizada
2. docker push asurbanipal1977/apidockerizada

### DESPLIEGUE EN AZURE
1. Vamos al portal Azure: https://portal.azure.com/#blade/HubsExtension/BrowseAll
2. Se crea un nuevo recurso y se selecciona Contenedores y Container Instance. Se indica que se quiere desplegar asurbanipal1977/apidockerizada desde hub.docker
3. La publicación en Azure está en http://20.74.56.247/weatherforecast
