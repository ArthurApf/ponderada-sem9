## Tutorial: Como dialogar com ambiente Cloud utilizando Terraform

### Instalando Terraform: 
Para instalação de Terraform, o primeiro passo é acessar a PowerShell do Windows, executando-a como administrador, mas IMPORTANTE: 

Ao executar a PowerShell, o diretório estará na pasta Systema32, é crucial que faça a instalação na raiz do disco.

Para instalar o Terraform, execute essa série de comandos na PowerShell:

~~~
Invoke-WebRequest -Uri https://releases.hashicorp.com/terraform/1.0.11/terraform_1.0.11_windows_amd64.zip -OutFile terraform.zip
~~~

~~~
Expand-Archive -Path terraform.zip -DestinationPath C:\terraform
~~~

~~~
[System.Environment]::SetEnvironmentVariable('PATH', $env:PATH + ';C:\terraform', [System.EnvironmentVariableTarget]::Machine)
~~~

Apenas cheque se o Terraform foi instalado a partir do comando no Terminal

~~~
Terraform -v 
~~~

### Instalando AWS CLI

Novamente, para realizar a instalação, o primeiro passo é executar o Windows PowerShell como administrador, e executar os comandos a seguir:

~~~
Invoke-WebRequest -Uri https://awscli.amazonaws.com/AWSCLIV2.msi -OutFile AWSCLIV2.msi
~~~

~~~
Start-Process msiexec.exe -Wait -ArgumentList '/I AWSCLIV2.msi /quiet'
~~~

Por fim, execute o comando para verficar a instalação 

~~~
aws --version
~~~


### Configurando AWS 

Vamos la! Com seu ambiente AWS, ou no caso do tutorial, o ambiente AWS Academy devidamente iniciado, abra o terminal na raiz do seu Armazenamento, execute o comando:

~~~
aws configure
~~~

Dentro do seu ambiente AWS Academy, acesse a aba AWS Details, e entre em AWS CLI, insira suas informações correspondete ao que o Terminal requisitar.

Seguindo, acesse seu diretório de usuário, e entre na pasta .aws, dentro dessa pasta no terminal, execute o comando:

~~~
notepad credentials
~~~

Dentro do notepad, altere o aws_session_token, copiando aquele presente dentro dos details do AWS Academy.

### Criando uma Instância EC2 com Terraform

O primeiro passo dessa etapa é adicionar, dentro de uma pasta de sua escolha, um arquivo

~~~
main.tf
~~~

Dentro desse arquivo, adicione o seguinte código:

~~~
provider "aws" {
  region = "us-east-1"
}

resource "aws_instance" "example" {
  ami           = "ami-0c02fb55956c7d316"  # Amazon Linux 2 AMI (HVM), SSD Volume Type
  instance_type = "t2.micro"

  tags = {
    Name = "TerraformExample"
  }
}
~~~

ATENTE-SE: 
Configure a variavel "region", de acordo com a região que sua maquina virtual está alocada.

Configure a variavel "instance_type", para o tipo de maquina virtual que for mais adequada para seu projeto, e para sua estimativa financeira. 

### Inicializando e Configurando o Terraform

No terminal, no diretório onde foi criado o arquivo main.tf, execute a série de comandos: 

~~~
terraform init
~~~

A partir disso a configuração ja estará pronta, mas é sempre bom para visualizar aquilo que será criado, execute o comando: 

~~~
terraform plan
~~~

E por fim, execute o comando: 

~~~
terraform apply
~~~

Digite "yes" quando for requisitado no terminal. 


### Finalizando o Terraform

Para finalizar o Terraform, basta executar no terminal, dentro do diretório onde se encontra o arquivo main.tf

~~~
terraform destroy
~~~
