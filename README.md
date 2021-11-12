Hola mundo en near con AssemblyScript
==================

Introducción a holamundo en near (assemblyScript)
==================

Este ejemplo se basa en un contrato escrito originalmente en Rust .

Desde el repositorio original (modificado ligeramente para mayor claridad):

    El contrato LinkDrop permite a cualquier usuario crear un enlace que sus amigos pueden usar para reclamar tokens incluso si aún no tienen una cuenta.

    Remitente (la persona que ya tiene CERCA de tokens):

        Crea un nuevo par de claves (public_key_1, private_key_1).
        Llamadas linkdrop.send(public_key_1)con el saldo adjunto de NEAR que quieren enviar.
        Envía el private_key_1a la persona que desea recibir los tokens (esto se puede hacer a través de cualquier aplicación de billetera compatible)

    Contrato Linkdrop (el contrato que ayuda a transferir NEAR entre el remitente y el destinatario)

        Captura el saldo adjunto del remitente como un nuevo registro asociado con public_key_1

    Receptor (la persona que aún no tiene NEAR)

        Recibe private_key_1(se puede hacer a través de cualquier aplicación de billetera compatible)
        Crea un nuevo par de claves (public_key_2, private_key_2).
        Decide un new_account_idquieren usar como su nueva cuenta.
        Llamadas linkdrop.create_account_and_claim(new_account_id, public_key_2)firmando mensaje con private_key_1

    Contrato de Linkdrop

        Crea una nueva cuenta nombrada por el valor de new_account_id
        Agrega public_key_2como clave de acceso total a la nueva cuenta
        Transfiere los tokens NEAR del remitente a la nueva cuenta

    SALIR

        El remitente ha enviado algunos tokens al receptor
        El receptor tiene una nueva cuenta cargada con tokens del remitente
        La experiencia del usuario del receptor es maravillosa

    Excepciones

        Si el receptor ya tiene una cuenta (o el remitente quiere recuperar el dinero), el remitente puede llamar linkdrop.claim()usando original private_key_1que transfiere dinero a la cuenta del firmante.



👨‍💻 Instalación en local
===========

Para correr este proyecto en local debes seguir los siguientes pasos:

Paso 1: Pre - Requisitos
------------------------------

1. Asegúrese de haber instalado [Node.js] ≥ 12 ((recomendamos usar [nvm])
2. Asegúrese de haber instalado yarn: `npm install -g yarn`
3. Instalar dependencias: `yarn install`
4. Crear un test near account [NEAR test account]
5. Instalar el NEAR CLI globally: [near-cli] es una interfaz de linea de comando (CLI) para interacturar con NEAR blockchain

    yarn install --global near-cli

Step 2: Configura tu NEAR CLI
-------------------------------

Configura tu near-cli para autorizar su cuenta de prueba creada recientemente:

    near login
    
Step 3: Clonar Repositorio
-------------------------------    

Este comando nos permite clonar el repositorio de nuestro proyecto 

```bash
git clone https://github.com/noemk2/holamundo_as.git
```

Una vez que hayas descargado el repositorio, asegurate de ejecutar los comandos dentro del repositorio descargado. Puedes hacerlo con
```bash
cd holamundo_as/
```

Step 4: Realiza el BUILD para implementación de desarrollo de contrato inteligente 
------------------------------------------------------------------------------------

Instale el gestor de dependencia de Node.js dentro del repositorio

```bash
npm install
```

Cree el código de contrato inteligente e implemente el servidor de desarrollo local: 
```bash
yarn deploy:dev
```

Cree la variable local $CONTRACT_NAME (permite guardar tu contrato temporal en una variable facil de recordar)
```bash
source ./neardev/dev-account.env
```

Consulte` package.json` para obtener una lista completa de `scripts` que puede ejecutar con` yarn`). Este script le devuelve un contrato inteligente provisional
implementado (guárdelo para
usarlo más tarde)


¡Felicitaciones, ahora tendrá un entorno de desarrollo local ejecutándose en NEAR TestNet!




✏️ Comando  view : request estatico
-----------------------------------------------

Permite imprimir "Hello world" 

Para Linux:
```bash
near view $CONTRACT_NAME hello_world --account-id <username>.testnet
```

✏️ Comando  call : request dinamico
--------------------------------------------

Permite imprimir "Hello " + <username>.testnet  

Para Linux :
```bash
near call $CONTRACT_NAME hello --account-id <username>.testnet
```


🤖 Test 
==================

Las pruebas son parte del desarrollo, luego, para ejecutar las pruebas en el contrato inteligente , debe ejecutar el siguiente comando:

    yarn test


==============================================

  [create-near-app]: https://github.com/near/create-near-app
  [Node.js]: https://nodejs.org/en/download/package-manager/
  [NEAR accounts]: https://docs.near.org/docs/concepts/account
  [NEAR Wallet]: https://wallet.testnet.near.org/
  [near-cli]: https://github.com/near/near-cli
  [NEAR test account]: https://docs.near.org/docs/develop/basics/create-account#creating-a-testnet-account
  [nvm]: https://github.com/nvm-sh/nvm
  [UX/UI]: https://www.figma.com/proto/GqP5EF5zRZRvAv3HoaSsuN/uniwap?node-id=39%3A2300&scaling=min-zoom&page-id=0%3A1&starting-point-node-id=39%3A2300&hide-ui=1
  [UX/UI]: https://www.figma.com/proto/0dZLC0WI1eVsfjeKu3T8J8/Garant%C3%ADzame?node-id=2%3A8&scaling=scale-down-width&page-id=0%3A1&starting-point-node-id=2%3A8
