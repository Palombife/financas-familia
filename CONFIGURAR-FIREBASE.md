# Ligar a sincronização (Firebase) — pelo celular, ~10 min

Gratuito para o uso de um casal. Faça **uma vez**, no celular de quem vai começar.

## 1. Criar o projeto
1. Abra https://console.firebase.google.com e entre com sua conta Google.
2. **Criar projeto** → nome: `nossas-financas` → pode desligar o Google Analytics → **Criar**.

## 2. Ativar o login anônimo
1. Menu **Build / Criação → Authentication → Vamos começar**.
2. Aba **Sign-in method** → **Anônimo** → ative → **Salvar**.

## 3. Criar o banco
1. Menu **Build → Firestore Database → Criar banco de dados**.
2. Local: `southamerica-east1 (São Paulo)` → modo **produção** → Criar.
3. Aba **Regras** → apague tudo e cole:
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /families/{family}/{document=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```
→ **Publicar**.

## 4. Pegar a configuração
1. Engrenagem ⚙️ → **Configurações do projeto** → role até **Seus apps** → ícone **`</>` (Web)**.
2. Apelido: `app` → **Registrar app** (não precisa de Hosting).
3. Copie o bloco `const firebaseConfig = { ... }`.

## 5. Ligar no app
1. No app: **Mais → Sincronização** → cole o bloco → **Conectar**.
2. Depois de conectar, aparece o **convite**. Toque em **WhatsApp** e envie para sua esposa.
3. No celular dela: abra o app → **Mais → Sincronização** → cole o convite → **Conectar**.

Pronto: lançamentos, metas e fotos de comprovantes aparecem nos dois celulares.

## Segurança
- O "código da família" (16 caracteres aleatórios) é a chave de acesso: só quem tem o convite lê os dados. Não compartilhe com mais ninguém.
- Os dados ficam no seu projeto Firebase, na sua conta Google.
- Para trocar o código ou revogar o acesso: **Desligar** no app e conecte de novo gerando outro código.
