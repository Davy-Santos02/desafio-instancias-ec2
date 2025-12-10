# Processamento Automático de Imagens com AWS (S3, Lambda, EC2 e EBS)

Este documento explica de forma simples e acessível como funciona uma arquitetura de **processamento automático de imagens** usando serviços da AWS. Mesmo quem nunca usou computação em nuvem consegue entender o fluxo.

---

## 📌 Visão Geral

O objetivo dessa arquitetura é receber uma imagem enviada por um usuário, processá-la automaticamente (por exemplo, redimensionar ou otimizar) e disponibilizar a versão final em um sistema.

Tudo isso acontece sem que nenhum desenvolvedor precise intervir manualmente.

---

## 🖼️ Diagrama da Arquitetura

O fluxo completo foi representado em um diagrama para facilitar a visualização:


(./images/Captura de tela 2025-12-10 144104.png)


---

## 🧩 Explicando Cada Componente

### **1. Usuário**

O usuário envia uma imagem através de um site, aplicativo ou sistema. Essa imagem precisa ser armazenada em algum lugar na nuvem.

---

### **2. Amazon S3 – Bucket de Upload**

O S3 funciona como um "Drive na nuvem", onde os arquivos ficam guardados.

Assim que a imagem chega:

* ela é armazenada com segurança
* gera um **evento automático** informando que um novo arquivo foi enviado

Esse evento é o que dispara o próximo passo.

---

### **3. AWS Lambda – Processamento Automático**

A Lambda funciona como um "pequeno programa" que roda automaticamente sem servidor.

Quando a imagem chega no S3, a Lambda é ativada e realiza tarefas como:

* Redimensionar a imagem
* Comprimir para reduzir tamanho
* Criar miniaturas (thumbnails)
* Validar formato

Tudo isso acontece em segundos e sem necessidade de infraestrutura dedicada.

---

### **4. Amazon S3 – Bucket Processado**

Depois de processada, a imagem final é enviada para outro bucket do S3.

Isso separa:

* imagens **originais**
* imagens **otimizadas/processadas**

Facilitando organização e segurança.

---

### **5. EC2 com EBS (Aplicação Web ou Painel)**

A instância EC2 representa um "servidor virtual" na AWS.

Ela acessa as imagens já processadas para:

* exibir ao usuário final
* servir em sites ou aplicações
* gerenciar uploads

O EBS funciona como o "disco rígido" desse servidor (onde ficam armazenados sistema, arquivos temporários, logs, etc.).

---

### **6. Usuário Final**

Depois que todo o processamento é concluído, o usuário visualiza a imagem otimizada em:

* sites web
* sistemas administrativos
* APIs
* aplicativos

---

## 🔄 Resumo do Fluxo Completo

1. Usuário envia uma imagem
2. S3 armazena e dispara evento
3. Lambda processa automaticamente
4. Imagem final volta para outro bucket S3
5. EC2 lê e entrega a imagem ao usuário final

Simples, automatizado e escalável.

---

## 🧠 Por que essa arquitetura é útil?

* Não precisa gerenciar servidores para processar imagens
* Escala automaticamente
* Baixo custo
* Separação organizada de arquivos
* Ótimo para portfólios, e-commerces, redes sociais, sistemas internos e muito mais


