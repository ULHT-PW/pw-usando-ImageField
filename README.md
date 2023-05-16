# Utilizando os campos ImageField e FileField num modelo 

Para adicionar um campo de imagem/ficheiro a uma classe, e manusear inserir imagens e ficheiros na base de dados através de formulários, deverá fazer os seguintes passos extra:

1. Criar, na root, a pasta `media/tarefas` para guardar os ficheiros carregados. Na pasta media deve colocar uma pasta com o nome da aplicação (no exemplo em baixo, aplicação tarefa).

```bash
> config
> media/tarefas
> tarefas
db.sqlite3
manage.py
```

2. Em `settings.py` adicionar referencia à pasta criada, com `MEDIA_URL` e `MEDIA_ROOT`:

```Python
MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
```

3. Em `config/urls.py` adicionar, depois de urlpatterns:

```Python
from django.conf import settings
from django.conf.urls.static import static

urlpatterns += static(
      settings.MEDIA_URL,
      document_root=settings.MEDIA_ROOT)
```

4. Em `models.py`, na classe adicionar um atributo com o campo imagem/ficheiro. Deverá especificar para onde devem ser carregados os ficheiros. O django como base a pasta media, neste caso ao especificar `upload_to='tarefas/'`, os ficheiros sendo carregados na pasta `media/tarefas/`.

```Python
imagem = models.ImageField(
             upload_to='tarefas/’, 
             null=True, 
             blank=True)
```

5. No ficheiro `views.py`, onde cria uma instância do formulário, adicionar `request.FILES`:

```Python
form = TarefaForm(request.POST or None, request.FILES)
```


6. No ficheiro HTML, no elemento `form` adicionar `enctype`:
```Python
<form method="POST" enctype="multipart/form-data">
```

