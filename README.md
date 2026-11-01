# Irmãos em Cristo – Luiz Cláudio

Projeto inicial de aplicativo de podcasts cristãos, com catálogo público, busca, player de áudio e painel administrativo protegido por login. O projeto vem com mensagens demonstrativas; os áudios reais entram depois, pelo painel.

## O que já está preparado
- Interface responsiva em português.
- Catálogo e busca de episódios.
- Player de áudio no aplicativo.
- Painel de administrador para publicar título, descrição, categoria e arquivo de áudio.
- Integração preparada com Supabase (banco + armazenamento na nuvem).
- Estrutura Capacitor para empacotar como aplicativo Android.

## Ativação do armazenamento (precisa ser feita pelo dono da conta)
1. Crie uma conta em https://supabase.com e um projeto.
2. No painel do projeto, abra **SQL Editor**, cole e execute todo o conteúdo de `supabase/schema.sql`.
3. Em **Project Settings → API**, copie o **Project URL** e a chave **anon/public**.
4. Abra `www/config.js` e cole os valores nos campos `SUPABASE_URL` e `SUPABASE_ANON_KEY`.
5. Em **Authentication → Users**, crie manualmente o usuário administrador com seu e-mail e uma senha forte. Deixe o cadastro público desativado.
6. A chave `anon/public` pode ficar no app; nunca coloque a `service_role` ou senha do painel no aplicativo.

## Testar no computador
Requer Node.js 20 ou superior.
```bash
npm install
npm run start
```
Abra o endereço local indicado pelo Vite. Sem configurar o Supabase, o app mostra apenas cartões de demonstração; o login e publicação ficam desativados.

## Gerar APK Android
Requer Android Studio, Android SDK e JDK 17 (ou a versão exigida pela instalação do Android Studio).
```bash
npm install
npm run build
npx cap add android
npx cap sync android
npx cap open android
```
No Android Studio, aguarde a sincronização do Gradle e use **Build → Build Bundle(s) / APK(s) → Build APK(s)**. O APK de teste costuma aparecer em `android/app/build/outputs/apk/debug/`.

## Importante sobre custos e limites
O plano gratuito do Supabase tem limites e condições que podem mudar. Áudio consome armazenamento e tráfego toda vez que alguém ouve/baixa. Confira os limites atuais em https://supabase.com/pricing antes de divulgar amplamente. Não há cobrança configurada por este projeto; não habilite upgrade pago sem conferir e autorizar.

## Segurança e publicação
As políticas SQL deste MVP permitem leitura pública e escrita para qualquer usuário autenticado. Portanto, mantenha a criação pública de contas desativada e crie apenas o seu usuário administrador. Para uma versão pública mais robusta, a próxima etapa é restringir a escrita ao UID do administrador e incluir moderação, exclusão segura de arquivos e recuperação de senha.
