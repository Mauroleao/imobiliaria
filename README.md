# Sistema de Gestão Imobiliária

Sistema web desenvolvido em Django para gerenciamento de propriedades imobiliárias, clientes, localizações e geração de relatórios.

## 📋 Descrição

Aplicação completa para gerenciar imóveis, registrar clientes e localizações, com funcionalidades de upload de imagens e geração de relatórios.

## 🛠️ Tecnologias

- **Python 3.x**
- **Django 4.1.3** - Framework web
- **Pillow 11.0.0** - Processamento de imagens
- **SQLite** - Banco de dados (padrão Django)

## 📦 Pré-requisitos

- Python 3.8 ou superior
- pip (gerenciador de pacotes Python)

## 🚀 Instalação Rápida

### 1. Clonar o repositório

```bash
git clone https://github.com/Mauroleao/imobiliaria.git
cd imobiliaria
```

### 2. Criar e Ativar Ambiente Virtual

**Windows:**
```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

**Linux/macOS:**
```bash
python -m venv .venv
source .venv/bin/activate
```

### 3. Instalar Dependências

```bash
pip install -r requirements.txt
```

### 4. Configurar Banco de Dados

```bash
python manage.py makemigrations
python manage.py migrate
```

### 5. Criar Superusuário (Administrador)

```bash
python manage.py createsuperuser
```

### 6. Rodar Servidor de Desenvolvimento

```bash
python manage.py runserver
```

Acesse em: http://127.0.0.1:8000/

## 📁 Estrutura do Projeto

```
imobiliaria/
├── core/                 # Configurações principais do projeto
│   ├── settings.py      # Configurações do Django
│   ├── urls.py          # Rotas principais
│   ├── asgi.py
│   └── wsgi.py
├── base/                 # App base com templates e static
│   ├── templates/       # Templates HTML compartilhados
│   ├── static/          # CSS, imagens compartilhadas
│   └── migrations/
├── myapp/               # App principal de imóveis
│   ├── models.py        # Modelos: Imóvel, Cliente, Localização, Imagem
│   ├── views.py         # Lógica da aplicação
│   ├── forms.py         # Formulários
│   ├── urls.py          # Rotas da aplicação
│   ├── templates/       # Templates específicos da app
│   ├── migrations/      # Histórico de mudanças no BD
│   └── admin.py         # Configuração do admin
├── manage.py            # Script de gerenciamento
└── requirements.txt     # Dependências do projeto
```

## 📝 Requisitos (requirements.txt)

A versão do **Pillow** foi atualizada para **11.0.0** para compatibilidade com versões atuais de Python e melhor performance no processamento de imagens.

```
asgiref==3.5.2
Django==4.1.3
Pillow==11.0.0
sqlparse==0.4.3
tzdata==2022.7
```

## 👤 Admin

Acesse o painel administrativo em: http://127.0.0.1:8000/admin

Use as credenciais do superusuário criado na instalação.

## 📚 Funcionalidades

- ✅ Cadastro e gestão de imóveis
- ✅ Gestão de clientes
- ✅ Registro de localizações
- ✅ Upload de imagens de imóveis
- ✅ Geração de relatórios
- ✅ Painel administrativo completo

## 🔧 Comandos Úteis

```bash
# Criar migrations
python manage.py makemigrations

# Aplicar migrations
python manage.py migrate

# Criar superusuário
python manage.py createsuperuser

# Rodar servidor
python manage.py runserver

# Acessar shell do Django
python manage.py shell

# Coletar arquivos estáticos (produção)
python manage.py collectstatic
```

## 📖 Referências

Desenvolvido com base em boas práticas de Django e estrutura MVC.
    
    “core” é nome do seu projeto e quando colocamos um “.” depois do nome do projeto significa que é para criar os arquivos na raiz da pasta. Assim não cria subpasta do projeto.
    
    ```python
    django-admin startproject core .
    ```
    
    **Testar a aplicação**
    
    ```python
    python manage.py runserver
    ```
    
</details>

<details><summary><b>Configurar Settings e Arquivos Static</b></summary>

- **Configurar Settings e Arquivos Static**
    
    ## **Vamos configurar nossos arquivos** *static*
    
    ```python
    import os 
    
    # base_dir config
    BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
    TEMPLATE_DIR = os.path.join(BASE_DIR,'templates')
    STATIC_DIR=os.path.join(BASE_DIR,'static')
    
    # Database
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.sqlite3',
            'NAME': os.path.join(BASE_DIR, 'db.sqlite3'), 
        }
    }
    
    STATIC_ROOT = os.path.join(BASE_DIR,'static')
    STATIC_URL = '/static/' 
    
    MEDIA_ROOT=os.path.join(BASE_DIR,'media')
    MEDIA_URL = '/media/'
    
    # Internationalization
    # Se quiser deixar em PT BR
    LANGUAGE_CODE = 'pt-br'
    TIME_ZONE = 'America/Sao_Paulo'
    USE_I18N = True
    USE_L10N = True 
    USE_TZ = True
    ```
    
    *myapp/urls.py*
    
    ```python
    from django.contrib import admin
    from django.conf import settings
    from django.conf.urls.static import static
    from django.urls import path
    
    urlpatterns = [
        path('admin/', admin.site.urls),
    ]
    
    urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT) # Adicionar Isto
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT) # Adicionar Isto
    ```
</details>

<details><summary><b>Criando Aplicativo</b></summary>

- **Criando Aplicativo**
    
    **Vamos criar nosso aplicativo no Django.**
    
    Para criar a aplicação no Django rode comando abaixo. “myapp” é nome do seu App.
    
    ```python
    python manage.py startapp myapp
    ```
    
    Agora precisamos registrar nossa aplicação no *INSTALLED_APPS* localizado em *settings.py*.
    
</details>

<details><summary><b>Template base e Bootstrap Configuração</b></summary>

- **Template base e Bootstrap Configuração**
    
    ### Bootstrap configuração
    
    Doc: [https://getbootstrap.com/docs/5.2/getting-started/introduction/](https://getbootstrap.com/docs/5.2/getting-started/introduction/)
    
    Com Base na documentação para utilizar os recursos Boostrap basta adicionar as tags de CSS e JS. No HTML da Pagina Base.
    
    ```python
    <!-- CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-rbsA2VBKQhggwzxH7pPCaAqO46MgnOM80zW1RWuH61DGLwZJEdK2Kadq2F9CUG65" crossorigin="anonymous">
    
    <!-- JS -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-kenU1KFdBIe4zVF0s0G1M5b4hcpxyD9F7jL+jjXkk+Q2h455rYXK/7HAuoJl+0I4" crossorigin="anonymous"></script>
    ```
    
    ## Template Base
    
    1 - criar um arquivo base ***base.html*** onde vamos renderizar nosso conteúdo. 
    
    ```python
    {% load static %}
    <!DOCTYPE html>
    <html lang="en">
    <head>
    	<meta charset="UTF-8">
    	<meta http-equiv="X-UA-Compatible" content="IE=edge">
    	<meta name="viewport" content="width=device-width, initial-scale=1.0">
    	<title>{% block title %}{% endblock %}</title>
    
    	<!-- CSS -->
    	<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-rbsA2VBKQhggwzxH7pPCaAqO46MgnOM80zW1RWuH61DGLwZJEdK2Kadq2F9CUG65" crossorigin="anonymous">
    
    </head>
    <body>  
    	
    	{% block content %}
    	
    	{% endblock %} 
     
    	<!-- JS-->
    	<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-kenU1KFdBIe4zVF0s0G1M5b4hcpxyD9F7jL+jjXkk+Q2h455rYXK/7HAuoJl+0I4" crossorigin="anonymous"></script>
    </body>
    </html>
    ```

</details>

<details><summary><b>Cria uma View</b></summary>

- **Cria uma View**
    
    *index1.html*
    
    ```html
    {% extends 'base.html' %}
    {% block title %}Pagina Inicial{% endblock %}
    {% block content %}
    	<h1>Pagina Inicial</h1>
    {% endblock %}
    ```
    
    *myapp/views.py*
    
    ```python
    from django.shortcuts import render
    
    # Create your views here.
    def mysite(request):
        return render(request, 'index1.html')
    ```
    
    criar arquivo *myapp*/*urls.py*
    
    ```
    from django.urls import path 
    from myapp import views
    
    urlpatterns = [
        path('', views.mysite, name='mysite'), 
    ]
    ```
    
    urls.py do projeto. ***core/urls.py***
    
    ```python
    from django.contrib import admin
    from django.urls import path, include # adicionar include
    from django.conf import settings
    from django.conf.urls.static import static 
    
    urlpatterns = [
        path('admin/', admin.site.urls),
        path('', include('myapp.urls')), # url do app
    ]
    urlpatterns += static(settings.STATIC_URL, document_root=settings.STATIC_ROOT) # Adicionar Isto
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT) # Adicionar Isto
    ```
    
    Rodar o projeto para ver como está.
    
    ```python
    python manage.py makemigrations && python manage.py migrate
    python manage.py runserver
    ```
    
    .gitignore
    
    ```python
    /tmp
    passenger_wsgi.py 
    .venv
    db.sqlite3
    /static_media
    static_media
    /static_files
    static_files
    /media
    mydatabase
    file_name.sql
    __pycache__ 
    __pycache__/
    ```

</details>
