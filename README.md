# pw-imagens

## Para gerir imagens e ficheiros na base de dados

1. Criar, na root, a pasta media/tarefas para guardar os ficheiros carregados. Na pasta media deve colocar uma pasta com o nome da aplicação (no exemplo em baixo, aplicação tarefa).

```bash
> config
> media/tarefas
> tarefas
db.sqlite3
manage.py
```

2. Em settings.py adicionar referencia à pasta criada, com MEDIA_URL e MEDIA_ROOT:

```Python
MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
```

3. Em config/urls.py adicionar, depois de urlpatterns:

```Python
from django.conf import settings
from django.conf.urls.static import static

urlpatterns += static(
      settings.MEDIA_URL,
      document_root=settings.MEDIA_ROOT)
```

4. Na view, quando cria uma instância do formulário, adicionar request.FILES:

```Python
form = TarefaForm(request.POST or None, request.FILES)
```

5. No template, no form adicionar enctype:

```Python
<form method="POST" enctype="multipart/form-data">
```

6. Em models, adicionar campo imagem/ficheiro

```Python
imagem = models.ImageField(
             upload_to='tarefas/’, 
             null=True, 
             blank=True)
```

