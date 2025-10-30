# 📝 Resumo da Implementação: AWS CloudFormation

Este documento resume a execução do laboratório prático de AWS CloudFormation, focado na aplicação dos conceitos de Infraestrutura como Código (IaC).

## 🎯 Objetivo da Implementação

Provisionar, de forma repetível e automatizada, um Bucket S3 configurado para Hospedagem de Site Estático.

## ⚙️ Template e Recursos Provisionados

O template `s3-website-template.yaml` define e provisiona os seguintes recursos, essenciais para o funcionamento do site estático:

| Recurso (Type) | Descrição | Configurações Críticas |
| :--- | :--- | :--- |
| `AWS::S3::Bucket` | Recurso de armazenamento de objetos. | Ativa a propriedade `WebsiteConfiguration` (definindo `index.html` e `error.html`). |
| `AWS::S3::BucketPolicy` | Recurso de permissão de acesso ao bucket. | Aplica a regra `s3:GetObject` para `Principal: *` (acesso público de leitura). |

### Funções Intrínsecas Utilizadas

* `!Ref`: Utilizada para referenciar o nome do Bucket S3 (gerado dinamicamente) dentro da `BucketPolicy` e na seção `Outputs`.
* `!GetAtt`: Utilizada para extrair o atributo `WebsiteURL` do Bucket S3 e exibi-lo na seção `Outputs`.

## 🔥 Principais Aprendizados (Insights de IaC)

1.  **Orquestração e Dependências:** A ferramenta CloudFormation gerencia automaticamente a ordem de *deploy* dos recursos. Ao usar `!Ref`, o sistema entende a dependência e garante que o recurso "pai" (Bucket) seja criado antes do recurso "filho" (Política de Bucket).
2.  **Imutabilidade e Segurança:** Em caso de falha durante a criação da *stack* (por erro de sintaxe ou configuração), o serviço executa o **Rollback Automático**, deletando todos os recursos incompletos e evitando o acúmulo de infraestrutura defeituosa (*lixo* ou *drift*).
3.  **Facilidade de Gestão (Outputs):** A seção `Outputs` é fundamental para extrair informações geradas pelo *deploy* (como a URL pública do site), centralizando dados críticos e agilizando a validação.

## 🚀 Conclusão

A prática demonstrou que o uso de templates CloudFormation transforma a infraestrutura em um ativo **declarativo**, garantindo **consistência** e **reprodutibilidade** em qualquer ambiente da AWS.
