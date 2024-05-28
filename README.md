# aws_cli
Guia  sobre o Uso do AWS CLI: Comandos Essenciais e Avançados



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
