# Build do 3105

Este repositório é uma cópia de trabalho independente do projeto original [YangJiiii/3105](https://github.com/YangJiiii/3105). A sincronização de conteúdo remoto do app usa o Worker `gh777-patch-feed`, ligado ao bucket R2 `gh777-patches-prod`.

## Compilação e sincronização remota

O projeto exige macOS, Xcode e o SDK iOS. O workflow [Build iOS app](.github/workflows/build-ios.yml) compila o target `worse_query` em `Release` e publica o artefato `external-gh777-ios-ipa`, contendo `EXTERNAL-GH777.ipa`, no run do GitHub Actions por 14 dias. O log bruto do Xcode não é anexado ao artefato.

O app consulta `https://gh777-patch-feed.marcelamartinszx12.workers.dev`, que lê o catálogo do bucket R2 privado `gh777-patches-prod` e disponibiliza o feed e os downloads em modo somente leitura. O app não recebe credenciais de escrita do R2 nem incorpora o antigo `PATCH_SYNC_TOKEN` na IPA. O acesso aos objetos passa pelo Worker; o bucket não é publicado diretamente.

## Instalação

O workflow desativa a assinatura (`CODE_SIGNING_ALLOWED=NO`). Embora o artefato tenha extensão `.ipa`, ele é um pacote não assinado e não pode ser instalado em um iPhone sem assinatura/provisionamento compatível. Certificados, perfis de provisionamento e distribuição não estão configurados neste repositório.
