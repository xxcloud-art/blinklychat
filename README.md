💬 Blinkly Chat App
Bem-vindo ao Blinkly, um aplicativo de chat em tempo real moderno e interativo, inspirado no Discord. Conecte-se com seus amigos em diversas salas, desde temas de jogos e programação até entretenimento!

✨ Funcionalidades
Autenticação de Usuário: Registro e login seguros com Firebase Authentication (e-mail/senha).

Perfis de Usuário: Nome de usuário e avatar dinâmico (gerado automaticamente).

Chat em Tempo Real: Envie e receba mensagens instantaneamente usando Socket.IO.

Salas de Chat: Participe de diferentes salas categorizadas (Games, Programação, Entretenimento).

Contagem de Usuários Online: Veja quantos usuários estão online em cada sala.

Histórico de Mensagens: As mensagens são persistidas e carregadas do Firestore Database.

Estado Online/Offline: Atualização de status de usuário (online/offline) em tempo real.

Interface Intuitiva: Design limpo e inspirado em plataformas populares de comunicação.

🚀 Tecnologias Utilizadas
Frontend:

HTML5: Estrutura das páginas.

CSS3: Estilização responsiva e moderna.

JavaScript (ES6+): Lógica do lado do cliente.

Firebase SDK (Client-side): Autenticação de usuário.

Socket.IO (Client): Conexão WebSocket para chat em tempo real.

Backend:

Node.js: Ambiente de execução do servidor.

Express.js: Framework web para o servidor REST API.

Socket.IO (Server):: Gerenciamento de conexões WebSocket.

Firebase Admin SDK: Interação segura com Firebase Authentication e Firestore Database.

Firestore Database: Banco de dados NoSQL para persistência de dados de usuários e mensagens.

⚙️ Configuração do Projeto (Local)
Para rodar o projeto em sua máquina local:

Clone o Repositório:

git clone https://github.com/SEU_USUARIO/blinkly-chat-app.git
cd blinkly-chat-app

(Lembre-se de substituir SEU_USUARIO e blinkly-chat-app pelo seu nome de usuário e nome do repositório no GitHub.)

Instale as Dependências do Backend:

npm install

Configuração do Firebase:

Crie um projeto no Console do Firebase.

Authentication: Habilite o método de login "Email/Password".

Firestore Database: Crie um banco de dados e configure as regras de segurança para permitir leitura/escrita por usuários autenticados (ver firestore-rules.md abaixo).

Service Account: No Firebase Console, vá em Project settings > Service accounts. Clique em Generate new private key para baixar seu arquivo firebase-service-account.json. Coloque este arquivo na raiz do seu projeto (blinkly-chat-app/).

Inicie o Servidor Backend:

node serve.js

O servidor estará rodando em http://localhost:3000.

Acesse o Frontend:

Abra seu navegador e vá para http://localhost:3000.

🔒 Regras do Firestore (firestore-rules.md)
Para que o aplicativo funcione corretamente, configure as seguintes regras no seu Firestore Database, na aba "Rules":

rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId} {
      allow read, write: if request.auth != null;
    }

    match /rooms/{roomId} {
      allow read, write: if request.auth != null;
      match /messages/{messageId} {
        allow read, write: if request.auth != null;
      }
    }
  }
}

🚀 Deployment Online (Vercel & Render)
Para colocar seu aplicativo online para você e seus amigos:

Frontend (Vercel):

Implante o conteúdo da sua pasta public/ no Vercel.

Certifique-se de configurar o "Root Directory" para public/.

Obtenha a URL do seu frontend (ex: https://blinkly-frontend.vercel.app).

Backend (Render):

Implante seu serve.js no Render como um "Web Service".

No seu serve.js, ajuste a inicialização do Firebase Admin SDK para ler a chave de serviço de uma variável de ambiente (não inclua o arquivo .json no seu repositório por segurança):

if (process.env.FIREBASE_SERVICE_ACCOUNT) {
    const serviceAccount = JSON.parse(process.env.FIREBASE_SERVICE_ACCOUNT);
    admin.initializeApp({ credential: admin.credential.cert(serviceAccount) });
}

No Render, adicione uma variável de ambiente:

Key: FIREBASE_SERVICE_ACCOUNT

Value: O conteúdo completo do seu arquivo firebase-service-account.json.

Obtenha a URL do seu backend (ex: https://blinkly-backend.onrender.com).

Atualize o Frontend (URL do Backend):

No seu arquivo public/feed.js, substitua http://localhost:3000 pela URL do seu backend implantado (Render):

const BACKEND_URL = 'https://blinkly-backend.onrender.com'; // Sua URL do Render
socket = io(BACKEND_URL, { /* ... */ });

Faça um git push dessa alteração para o seu repositório, e o Vercel fará um novo deploy automático do seu frontend.

📸 Screenshots (Opcional)
(Você pode adicionar capturas de tela do seu aplicativo aqui para mostrar como ele se parece. Ex:)
*
