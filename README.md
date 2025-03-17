# Protetor de Link

[Proteger links com senha através do navegador]
Github original (https://jstrieb.github.io/link-lock)

Fork criado para complementar websites criados em Português Brasileiro.



## Sobre

O Protetor de Link é uma ferramenta para criptografar e descriptografar URLs. Quando um usuário acessa uma URL criptografada, será solicitada uma senha. Se a senha estiver correta, o Protetor de Link recupera a URL original e redireciona o usuário para ela. Caso contrário, uma mensagem de erro será exibida. Os usuários também podem adicionar dicas que serão exibidas próximas ao campo da senha.

Cada URL criptografada é armazenada inteiramente dentro do link gerado pela aplicação. Por isso, os usuários têm controle total sobre os dados que criam com o Protetor de Link. Nada é armazenado em servidores, e não há uso de cookies, rastreamento ou cadastros.

O Protetor de Link possui muitas utilidades:

- Armazenar favoritos privados em computadores compartilhados
- Criptografar páginas web inteiras (através das [URL Pages](https://github.com/jstrieb/urlpages))
- Enviar links sensíveis por canais públicos ou inseguros (por exemplo, publicar links em sites públicos que exijam senha para acesso)
- Implementar CAPTCHAs simples – especialmente eficazes contra web scrapers básicos que não respeitam o `robots.txt`
- Adicionar uma senha a links compartilhados do Dropbox ou Google Drive
- Compartilhar links magnéticos ou torrents protegidos por senha
- [Contornar censura](#evading-censorship)

O Protetor de Link utiliza AES no modo GCM para criptografar senhas de forma segura, além de PBKDF2 e SHA-256 com salt (100.000 iterações) para derivação segura da chave. A criptografia, a descriptografia e a derivação das chaves são feitas pelo [SubtleCrypto API](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto). O vetor de inicialização é aleatório por padrão, mas o salt não é. A randomização tanto do vetor de inicialização quanto do salt pode ser ativada ou desativada pelo usuário nas "opções avançadas". O salt e o vetor de inicialização são enviados junto com os dados criptografados caso tenham sido gerados aleatoriamente. A API possui versionamento, garantindo que links criptografados antigos continuem funcionando, mesmo se futuras versões do Protetor de Link forem atualizadas com segurança aprimorada. Para mais informações, leia o código ([`api.js`](https://github.com/jstrieb/link-lock/blob/master/api.js), especialmente).

Leia a discussão no Hacker News [aqui](https://news.ycombinator.com/item?id=23242290).

Também discutido no [r/netsec](https://www.reddit.com/r/netsec/comments/i3n4sm/link_lock_password_protect_urls_using_aes_in_the/) e no [r/programming](https://www.reddit.com/r/programming/comments/i5kpjx/link_lock_is_a_tool_for_encrypting_and_decrypting/).



## Aviso

O código foi escrito para ser lido. Recomendo que você o leia, especialmente se não confiar em mim para desenvolver uma aplicação segura de criptografia. Em especial:

- Uma vez que alguém descriptografe um link, poderá compartilhar a URL original livremente. Compartilhe links criptografados apenas com pessoas de confiança.
- A maior parte do código de criptografia e descriptografia é baseada nos [tutoriais da MDN](https://developer.mozilla.org/en-US/docs/Web/API/SubtleCrypto/deriveKey#PBKDF2_2) para a API `SubtleCrypto`.



## Uso

- Crie um link protegido aqui: [https://jstrieb.github.io/link-lock](https://jstrieb.github.io/link-lock).
- Após criar um link protegido, crie um favorito oculto aqui:
  <https://jstrieb.github.io/link-lock/hidden>.
- Utilize as opções avançadas ao criar um link para aumentar a segurança da criptografia (ao custo de gerar um link mais longo).
    - Por padrão, o vetor de inicialização é aleatório para maior segurança, mas isso pode ser desativado, apesar de representar uma vulnerabilidade.
    - Por padrão, o salt utilizado para gerar o hash da senha durante a derivação da chave não é aleatório, mas isso pode ser ativado.
- Para adicionar aos favoritos um link protegido, arraste-o da caixa de saída até a barra de favoritos. Alternativamente, visite o link protegido e marque-o antes de inserir a senha.
- Caso perca a senha, é praticamente impossível recuperar o link original. A segurança robusta garantida pela criptografia pode ser uma bênção ou um problema caso você não tenha cuidado!
- Atualmente, a única maneira de recuperar uma senha perdida é testando todas as opções possíveis por força bruta (muito lentamente). Um exemplo de aplicação para tentar descobrir URLs do Protetor de Link por força bruta no navegador pode ser encontrado aqui:
  <https://jstrieb.github.io/link-lock/bruteforce>.
- Um aplicativo paralelo, multiplataforma e baseado em CPU para força bruta pode ser encontrado aqui:
  <https://github.com/jstrieb/bruteforce-link-lock>
- Se você receber uma URL do Protetor de Link na qual não confia, descriptografe-a usando esta interface que não redireciona automaticamente:
  <https://jstrieb.github.io/link-lock/decrypt>.




## Outras versões e projetos relacionados
- Projeto original:
  [https://jstrieb.github.io/link-lock/](https://jstrieb.github.io/link-lock)
- Versão em francês:
  [cachetonsite.di20.net](https://cachetonsite.di20.net)
- Versão em alemão:
  [ebildungslabor.github.io/link-lock](https://ebildungslabor.github.io/link-lock/)
- Versão em polonês: 
  [yoursenseicreeper.github.io/link-lock](https://yoursenseicreeper.github.io/link-lock/)
