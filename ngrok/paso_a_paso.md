Paso a paso para instalar y habilitar el Ngrok

Entrar a la pagina de ngrok para poder crear el tunel (https://dashboard.ngrok.com/get-started/setup/windows)

Aqui lo que haremos sera logearnos con nuestra cuenta para habilitar el servicio de tunel authentoken.

Posterior en simbolos de sistema:

cd // para ir a directorio raiz de la maquina servidor

wget https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip // este comando es para descargar el Ngrok 

unzip ngrok-stable-linux-amd64.zip // este comando es para descomprimir el archvo de Ngrok


./ngrok // Sirve para verificar el estado del ngrok

Posterios a estos pasos vamos a obtener el autentificador de ngrok, en nuestro caso es el siguiente, pero deberia lucir algo asi:

ngrok config add-authtoken 2dIUq0RQPHPIuaFTTagUgGMq1HW_5vuqmJ6pq5hkNB7JRmuCH // Con este comando en smd nos debe aparecer algo tal que asi:

Usage of ngrok requires a verified account and authtoken.

Sign up for an account: https://dashboard.ngrok.com/signup
Install your authtoken: https://dashboard.ngrok.com/get-started/your-authtoken

ERR_NGROK_4018  // Con este error accederemos al link que se muestra en Install your authtoken, esto el fin de ingresar a la pagina de acceso para obtener nuevamente el authtoken

Finalmente:

ngrok http http://localhost:8080 // Con este comando accederemos a la pagina que nos redireccionara para crear el Tunel de conexion de nuestro servidor local a la red local.

Ya con este paso a paso deberias poder visualizar desde otro pc la pagina creada..

Juan Pulido
Sergio Cardenas
