# pw-imagens

## Para gerir imagens e ficheiros na base de dados

1. Criar, na root, a pasta media/tarefas para guardar os ficheiros carregados. Na pasta media deve colocar uma pasta com o nome da aplicação (no exemplo em baixo, aplicação tarefa)

![image](https://github.com/ULHT-PW/pw-imagens/assets/42048382/b68d9e41-e6c6-4200-84a6-7a9d037594a1)

2. Em settings.py adicionar MEDIA_URL e MEDIA_ROOT:

```Python
MEDIA_URL = '/media/'
MEDIA_ROOT = os.path.join(BASE_DIR, 'media')
```

3. Em config/urls.py adicionar static():

```Python
from django.conf import settings
from django.conf.urls.static import static

urlpatterns += static(
      settings.MEDIA_URL,
      document_root=settings.MEDIA_ROOT)
```

4. Na view adicionar request.FILES:
```Python
form = TarefaForm(request.POST or None, request.FILES)
```

5. No template, no form adicionar ecntype:
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

