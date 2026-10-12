# Ligar a sincronização (Firebase) — pelo celular, ~10 min

Gratuito para o uso de um casal. Faça **uma vez**, no celular de quem vai começar.
Cada um entra com a **própria conta** (Google ou e-mail e senha), e só os **2 e-mails de vocês** acessam os dados.

## 1. Criar o projeto
1. Abra https://console.firebase.google.com e entre com sua conta Google.
2. **Criar projeto** → nome: `nossas-financas` → desligue o Google Analytics → **Criar**.

## 2. Ativar o login
1. Menu **Build / Criação → Authentication → Vamos começar**.
2. Aba **Sign-in method**: ative **Google** (escolha seu e-mail de suporte → Salvar) e ative **E-mail/senha** (só a 1ª chave, não a de "link por e-mail") → Salvar.
3. Aba **Settings / Configurações → Authorized domains / Domínios autorizados → Adicionar domínio**: `palombife.github.io`.

## 3. Criar o banco e liberar só vocês dois
1. Menu **Build → Firestore Database → Criar banco de dados**.
2. Local: `southamerica-east1 (São Paulo)` → modo **produção** → Criar.
3. Aba **Regras** → apague tudo e cole, **trocando os dois e-mails pelos de vocês (minúsculas)**:
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /casal/{document=**} {
      allow read, write: if request.auth != null
        && request.auth.token.email_verified == true
        && request.auth.token.email in ['SEU_EMAIL@gmail.com', 'EMAIL_DELA@gmail.com'];
    }
  }
}
```
→ **Publicar**.

## 4. Pegar a configuração
1. Engrenagem ⚙️ → **Configurações do projeto** → **Seus apps** → ícone **`</>` (Web)**.
2. Apelido: `app` → **Registrar app** (sem Hosting).
3. Copie o bloco `const firebaseConfig = { ... }`.

## 5. Ligar no app
1. **Mais → Sincronização** → cole o bloco → **Conectar**.
2. Entre com Google (ou e-mail e senha — vai chegar um e-mail para confirmar).
3. Em **Mais → Sincronização** aparece o **convite**. Toque em **WhatsApp** e mande para ela.
4. No celular dela: abra o app → **Mais → Sincronização** → cole o convite → **Conectar** → entre com o e-mail dela (o mesmo que está nas regras).

## Segurança
- O convite leva só a configuração do app (não é senha). Sem e-mail liberado nas regras, ninguém lê os dados.
- Para liberar/tirar alguém: edite a lista de e-mails nas **Regras** e publique.
- Dica: no iPhone, o botão do Google pode falhar se o app estiver aberto pelo ícone da tela inicial. Nesse caso use **e-mail e senha**.
