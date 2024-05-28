# aws_cli
Guia  sobre o Uso do AWS CLI: Comandos Essenciais e Avançados

### Guia Completo sobre o Uso do AWS CLI: Comandos Essenciais e Avançados

A AWS Command Line Interface (CLI) é uma ferramenta poderosa que permite interagir com os serviços da AWS diretamente do seu terminal. Desde tarefas básicas até operações avançadas, o AWS CLI pode facilitar muito o gerenciamento dos recursos na nuvem. Este artigo abordará os principais comandos que você deve conhecer, desde os mais básicos até os avançados, para aproveitar ao máximo a AWS CLI.

### Configuração Inicial

Antes de explorar os comandos, é necessário configurar o AWS CLI com suas credenciais. As chaves de acesso da AWS (Access Key ID e Secret Access Key) são essenciais para autenticar e autorizar suas solicitações à AWS.

- **Access Key ID**: Um identificador único para a chave de acesso.
- **Secret Access Key**: Um segredo usado para assinar suas solicitações para a AWS.

Para configurar o AWS CLI com suas credenciais, use o seguinte comando:

```
aws configure

```

Você será solicitado a fornecer:

- **AWS Access Key ID**
- **AWS Secret Access Key**
- **Default region name** (ex: us-east-1)
- **Default output format** (json, text, table)

### Comandos Essenciais do AWS CLI

1. **`aws sts get-caller-identity`**
    - **Descrição**: Retorna detalhes sobre a entidade AWS que está fazendo a chamada à API.
    - **Exemplo**:
        
        ```
        aws sts get-caller-identity
        
        ```
        
    - **Uso**: Verificar qual usuário ou role está autenticado.
2. **`aws s3 ls`**
    - **Descrição**: Lista todos os buckets S3 em sua conta.
    - **Exemplo**:
        
        ```
        aws s3 ls
        
        ```
        
    - **Uso**: Visualizar os buckets disponíveis.
3. **`aws ec2 describe-instances`**
    - **Descrição**: Lista todas as instâncias EC2 em sua conta.
    - **Exemplo**:
        
        ```
        aws ec2 describe-instances
        
        ```
        
    - **Uso**: Obter detalhes sobre suas instâncias EC2.
4. **`aws s3 cp`**
    - **Descrição**: Copia arquivos entre seu sistema local e um bucket S3.
    - **Exemplo**:
        
        ```
        aws s3 cp myfile.txt s3://mybucket/myfile.txt
        
        ```
        
    - **Uso**: Transferir arquivos para e do S3.
    - **Opções adicionais**: Use `-recursive` para copiar diretórios inteiros.
        
        ```
        aws s3 cp mydir s3://mybucket/mydir --recursive
        
        ```
        
5. **`aws ec2 start-instances`**
    - **Descrição**: Inicia uma ou mais instâncias EC2.
    - **Exemplo**:
        
        ```
        aws ec2 start-instances --instance-ids i-1234567890abcdef0
        
        ```
        
    - **Uso**: Iniciar instâncias EC2 específicas.
6. **`aws ec2 stop-instances`**
    - **Descrição**: Para uma ou mais instâncias EC2.
    - **Exemplo**:
        
        ```
        aws ec2 stop-instances --instance-ids i-1234567890abcdef0
        
        ```
        
    - **Uso**: Parar instâncias EC2 específicas.
7. **`aws iam list-users`**
    - **Descrição**: Lista todos os usuários IAM na sua conta.
    - **Exemplo**:
        
        ```
        aws iam list-users
        
        ```
        
    - **Uso**: Gerenciar usuários IAM.
8. **`aws lambda invoke`**
    - **Descrição**: Invoca uma função Lambda e retorna a resposta.
    - **Exemplo**:
        
        ```
        aws lambda invoke --function-name MyFunction output.txt
        
        ```
        
    - **Uso**: Executar funções Lambda e verificar suas respostas.
9. **`aws dynamodb scan`**
    - **Descrição**: Escaneia uma tabela DynamoDB e retorna os itens correspondentes.
    - **Exemplo**:
        
        ```
        aws dynamodb scan --table-name MyTable
        
        ```
        
    - **Uso**: Obter todos os itens de uma tabela DynamoDB.
10. **`aws cloudformation deploy`**
    - **Descrição**: Implanta um stack do AWS CloudFormation.
    - **Exemplo**:
        
        ```
        aws cloudformation deploy --template-file mytemplate.yaml --stack-name mystack
        
        ```
        
    - **Uso**: Gerenciar stacks do CloudFormation.

### Comandos Avançados do AWS CLI

Além dos comandos essenciais, há comandos mais avançados que podem ser extremamente úteis para administradores de sistemas e desenvolvedores:

1. **`aws s3 sync`**
    - **Descrição**: Sincroniza diretórios locais com buckets S3.
    - **Exemplo**:
        
        ```
        aws s3 sync . s3://mybucket
        
        ```
        
    - **Uso**: Backup e sincronização de dados.
2. **`aws cloudwatch get-metric-statistics`**
    - **Descrição**: Obtém estatísticas para uma métrica do CloudWatch.
    - **Exemplo**:
        
        ```
        aws cloudwatch get-metric-statistics --metric-name CPUUtilization --start-time 2023-05-26T00:00:00Z --end-time 2023-05-26T23:59:59Z --period 3600 --namespace AWS/EC2 --statistics Average
        
        ```
        
    - **Uso**: Monitoramento detalhado de recursos.
3. **`aws rds describe-db-instances`**
    - **Descrição**: Lista todas as instâncias de banco de dados RDS.
    - **Exemplo**:
        
        ```
        aws rds describe-db-instances
        
        ```
        
    - **Uso**: Gerenciamento de bancos de dados RDS.
4. **`aws ecs list-clusters`**
    - **Descrição**: Lista todos os clusters ECS.
    - **Exemplo**:
        
        ```
        aws ecs list-clusters
        
        ```
        
    - **Uso**: Gerenciamento de clusters ECS.
5. *



### Mais Dicas e Práticas para Maximizar o Uso do AWS CLI

#### Automação e Integração

O AWS CLI é especialmente útil quando integrado com ferramentas de automação e scripts. Abaixo estão algumas práticas recomendadas para integrar e automatizar tarefas usando o AWS CLI:

1. **Uso de Variáveis de Ambiente**:
   - Configure suas credenciais e região através de variáveis de ambiente para scripts reutilizáveis:
     ```sh
     export AWS_ACCESS_KEY_ID=your_access_key_id
     export AWS_SECRET_ACCESS_KEY=your_secret_access_key
     export AWS_DEFAULT_REGION=us-east-1
     ```

2. **Uso de IAM Roles com EC2**:
   - Ao executar scripts em instâncias EC2, utilize IAM roles associadas às instâncias em vez de credenciais estáticas, para aumentar a segurança e simplificar o gerenciamento de credenciais.

3. **Agendamento de Tarefas com cron**:
   - Utilize o cron para agendar tarefas automatizadas no Linux. Por exemplo, fazer backup de um diretório para o S3 diariamente:
     ```sh
     0 2 * * * /usr/bin/aws s3 sync /local/dir s3://mybucket/backup --delete
     ```

4. **Integração com CI/CD**:
   - Integre o AWS CLI em pipelines CI/CD para automação de deploys e gerenciamento de infraestrutura. Ferramentas como Jenkins, GitLab CI, e AWS CodePipeline suportam execução de scripts com AWS CLI.

5. **Logging e Monitoramento**:
   - Redirecione a saída de comandos para arquivos de log para monitoramento e auditoria.
     ```sh
     aws s3 sync /local/dir s3://mybucket/backup --delete >> /var/log/s3sync.log 2>&1
     ```

#### Comandos Úteis para Administradores de Sistemas

1. **`aws ec2 reboot-instances`**
   - **Descrição**: Reinicia uma ou mais instâncias EC2.
   - **Exemplo**:
     ```sh
     aws ec2 reboot-instances --instance-ids i-1234567890abcdef0
     ```

2. **`aws cloudwatch put-metric-alarm`**
   - **Descrição**: Cria ou atualiza um alarme no CloudWatch.
   - **Exemplo**:
     ```sh
     aws cloudwatch put-metric-alarm --alarm-name HighCPUUsage --metric-name CPUUtilization --namespace AWS/EC2 --statistic Average --period 300 --threshold 80 --comparison-operator GreaterThanOrEqualToThreshold --evaluation-periods 1 --alarm-actions arn:aws:sns:us-east-1:123456789012:MyTopic --dimensions Name=InstanceId,Value=i-1234567890abcdef0
     ```

3. **`aws sns publish`**
   - **Descrição**: Envia uma mensagem para um tópico SNS.
   - **Exemplo**:
     ```sh
     aws sns publish --topic-arn arn:aws:sns:us-east-1:123456789012:MyTopic --message "Deployment completed successfully."
     ```

4. **`aws ec2 describe-snapshots`**
   - **Descrição**: Lista os snapshots EBS na sua conta.
   - **Exemplo**:
     ```sh
     aws ec2 describe-snapshots --owner-ids self
     ```

5. **`aws rds create-db-snapshot`**
   - **Descrição**: Cria um snapshot de uma instância de banco de dados RDS.
   - **Exemplo**:
     ```sh
     aws rds create-db-snapshot --db-instance-identifier mydbinstance --db-snapshot-identifier mydbsnapshot
     ```

#### Boas Práticas de Segurança

1. **Políticas de Menor Privilégio**:
   - Sempre aplique o princípio do menor privilégio ao criar políticas IAM para usuários e roles que utilizarão o AWS CLI.

2. **Rotação de Credenciais**:
   - Rotacione regularmente suas chaves de acesso para minimizar o risco de comprometimento.

3. **Uso de MFA**:
   - Implemente autenticação multifator (MFA) para usuários IAM para adicionar uma camada extra de segurança.

4. **Gerenciamento de Perfis**:
   - Utilize diferentes perfis para separar ambientes (ex: desenvolvimento, produção) e evite uso de credenciais estáticas em scripts:
     ```sh
     aws configure --profile dev
     aws configure --profile prod
     ```

#### Recursos Adicionais e Documentação

1. **Documentação Oficial da AWS CLI**:
   - Acesse a [documentação oficial](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html) para detalhes completos sobre comandos e opções.

2. **AWS CLI Cheatsheet**:
   - Utilize cheatsheets para acesso rápido a comandos comuns e suas opções.

3. **Tutoriais e Workshops**:
   - Participe de tutoriais e workshops para aprimorar suas habilidades com o AWS CLI e explorar casos de uso avançados.

### Conclusão

O AWS CLI é uma ferramenta indispensável para quem trabalha com AWS, oferecendo um nível de controle e automação que não é possível através do Console da AWS. Conhecer e utilizar esses comandos pode melhorar significativamente sua eficiência e eficácia no gerenciamento dos serviços AWS. Com prática e exploração contínua, você pode descobrir ainda mais funcionalidades e comandos que se adaptam às suas necessidades específicas. Ao seguir as práticas recomendadas e integrar o AWS CLI em seus fluxos de trabalho, você pode maximizar a produtividade e segurança na gestão da infraestrutura em nuvem.
