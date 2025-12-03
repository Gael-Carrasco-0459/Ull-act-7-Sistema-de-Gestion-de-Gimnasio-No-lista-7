---
UIII_Gym_0459/
├── .venv/                              <-- Entorno Virtual
├── backend_gimnasio07/                 <-- Configuración del Proyecto
│   ├── __init__.py
│   ├── asgi.py
│   ├── settings.py                     <-- Aquí registraste 'members'
│   ├── urls.py                         <-- Aquí incluiste members.urls
│   └── wsgi.py
├── members/                            <-- Tu Aplicación
│   ├── migrations/                     <-- Archivos de migraciones de la BD
│   ├── templates/                      <-- Carpeta principal de HTMLs
│   │   ├── clase/
│   │   │   ├── actualizar_clase.html
│   │   │   ├── agregar_clase.html
│   │   │   ├── borrar_clase.html
│   │   │   └── ver_clases.html
│   │   ├── entrenador/
│   │   │   ├── actualizar_entrenador.html
│   │   │   ├── agregar_entrenador.html
│   │   │   ├── borrar_entrenador.html
│   │   │   └── ver_entrenadores.html
│   │   ├── membresia/
│   │   │   ├── actualizar_membresia.html
│   │   │   ├── agregar_membresia.html
│   │   │   ├── borrar_membresia.html
│   │   │   └── ver_membresias.html
│   │   ├── pago/
│   │   │   ├── actualizar_pago.html
│   │   │   ├── agregar_pago.html
│   │   │   ├── borrar_pago.html
│   │   │   └── ver_pagos.html
│   │   ├── reserva_clase/
│   │   │   ├── actualizar_reserva_clase.html
│   │   │   ├── agregar_reserva_clase.html
│   │   │   ├── borrar_reserva_clase.html
│   │   │   └── ver_reservas_clase.html
│   │   ├── rutina_personalizada/
│   │   │   ├── actualizar_rutina_personalizada.html
│   │   │   ├── agregar_rutina_personalizada.html
│   │   │   ├── borrar_rutina_personalizada.html
│   │   │   └── ver_rutinas_personalizadas.html
│   │   ├── socio/
│   │   │   ├── actualizar_socio.html
│   │   │   ├── agregar_socio.html
│   │   │   ├── borrar_socio.html
│   │   │   └── ver_socios.html
│   │   ├── base.html                   <-- Plantilla madre
│   │   ├── footer.html                 <-- Pie de página
│   │   ├── header.html                 <-- Encabezado (Logo/Título)
│   │   ├── inicio.html                 <-- Página de Bienvenida
│   │   └── navbar.html                 <-- Menú de navegación
│   ├── __init__.py
│   ├── admin.py                        <-- Registro de modelos en panel admin
│   ├── apps.py
│   ├── models.py                       <-- Definición de las 7 tablas
│   ├── urls.py                         <-- Rutas de la app members
│   └── views.py                        <-- Lógica (Funciones CRUD)
├── db.sqlite3                          <-- Base de datos (se crea al migrar)
└── manage.py                           <-- Ejecutor de comandos
---

Aquí tienes la guía completa paso a paso para desarrollar el proyecto **Gym Flame** con Django, siguiendo estrictamente tus requerimientos, estructura de carpetas y lógica sin formularios de Django (`forms.py`).

Debido a la extensión del código (7 modelos x 4 vistas x 4 templates), te proporcionaré la estructura funcional completa, la configuración, los modelos, las vistas y URLs completas, y los templates base más los ejemplos completos para "Membresía" y "Socio" (que incluye claves foráneas). Para el resto (Entrenador, Clase, etc.), el código HTML es repetitivo, por lo que te indicaré cómo replicarlo fácilmente.

---

### Parte 1: Configuración Inicial (Pasos 1-11)

**1. Crear carpeta del Proyecto:**
Abre tu explorador de archivos o terminal y crea la carpeta.
```bash
mkdir UIII_Gym_0459
```

**2. Abrir VS Code sobre la carpeta:**
Abre VS Code, ve a `Archivo > Abrir Carpeta` y selecciona `UIII_Gym_0459`.

**3. Abrir terminal en VS Code:**
Presiona `` Ctrl + ` `` (control + acento grave) o ve al menú `Ver > Terminal`.

**4. Crear entorno virtual:**
En la terminal, escribe:
```bash
python -m venv .venv
```

**5. Activar entorno virtual:**
*   **Windows:** `.venv\Scripts\activate`
*   **Mac/Linux:** `source .venv/bin/activate`
*(Verás que aparece `(.venv)` al inicio de la línea de comandos).*

**6. Activar intérprete de Python:**
Presiona `Ctrl + Shift + P` > Escribe `Python: Select Interpreter` > Selecciona la opción que dice `('.venv': venv)`.

**7. Instalar Django:**
```bash
pip install django
```

**8. Crear proyecto sin duplicar carpeta:**
El punto `.` al final es importante para no crear una subcarpeta extra.
```bash
django-admin startproject backend_gimnasio07 .
```

**9. Ejecutar servidor en puerto 8059:**
```bash
python manage.py runserver 8059
```

**10. Ver en navegador:**
Copia y pega `http://127.0.0.1:8059/` en tu navegador. Deberías ver el cohete de Django. (Presiona `Ctrl+C` en la terminal para detenerlo y seguir trabajando).

**11. Crear aplicación `members`:**
```bash
python manage.py startapp members
```

---

### Parte 2: Configuración del Proyecto (Backend)

**25, 31, 36... Agregar app en `settings.py`:**
Abre `backend_gimnasio07/settings.py` y busca `INSTALLED_APPS`. Agrega `'members',`:

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'members', # <--- Agregado aquí
]
```

**24, 30... Configurar `urls.py` principal:**
Abre `backend_gimnasio07/urls.py` y modifícalo para incluir las URLs de la app:

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('members.urls')),
]
```

---

### Parte 3: Base de Datos (Modelos)

**12. Definir Modelos en `members/models.py`:**
Copia y pega el código que proporcionaste. Asegúrate de tener los imports correctos.

```python
from django.db import models

# --- MEMBRESIA ---
class Membresia(models.Model):
    tipo_membresia = models.CharField(max_length=50, verbose_name="Tipo de Membresía")
    descripcion = models.TextField(verbose_name="Descripción")
    costo = models.DecimalField(max_digits=10, decimal_places=2)
    duracion_meses = models.IntegerField(verbose_name="Duración (Meses)")
    beneficios = models.TextField()
    num_sesiones_incluidas = models.IntegerField(verbose_name="Número de Sesiones")
    es_activa = models.BooleanField(default=True, verbose_name="¿Está activa?")

    def __str__(self):
        return f"{self.tipo_membresia} - ${self.costo}"

    class Meta:
        verbose_name = "Membresía"
        verbose_name_plural = "Membresías"

# --- SOCIO ---
class Socio(models.Model):
    GENERO_CHOICES = [('M', 'Masculino'), ('F', 'Femenino'), ('O', 'Otro')]
    nombre = models.CharField(max_length=100)
    apellido = models.CharField(max_length=100)
    fecha_nacimiento = models.DateField()
    genero = models.CharField(max_length=1, choices=GENERO_CHOICES)
    direccion = models.CharField(max_length=255)
    telefono = models.CharField(max_length=20)
    email = models.EmailField(max_length=100)
    fecha_registro = models.DateField(auto_now_add=True)
    membresia = models.ForeignKey(Membresia, on_delete=models.SET_NULL, null=True, related_name="socios")
    fecha_vencimiento_membresia = models.DateField()

    def __str__(self):
        return f"{self.nombre} {self.apellido}"

# --- ENTRENADOR ---
class Entrenador(models.Model):
    nombre = models.CharField(max_length=100)
    apellido = models.CharField(max_length=100)
    especialidad = models.CharField(max_length=100)
    telefono = models.CharField(max_length=20)
    email = models.EmailField(max_length=100)
    fecha_contratacion = models.DateField()
    salario = models.DecimalField(max_digits=10, decimal_places=2)
    certificado = models.CharField(max_length=100)

    def __str__(self):
        return f"{self.nombre} {self.apellido} - {self.especialidad}"
    class Meta:
        verbose_name_plural = "Entrenadores"

# --- CLASE ---
class Clase(models.Model):
    nombre_clase = models.CharField(max_length=100)
    descripcion = models.TextField()
    horario = models.CharField(max_length=100, help_text="Ej: Lunes y Miércoles 10:00 AM")
    duracion_minutos = models.IntegerField()
    entrenador = models.ForeignKey(Entrenador, on_delete=models.SET_NULL, null=True, related_name="clases")
    cupo_maximo = models.IntegerField()
    costo_clase = models.DecimalField(max_digits=10, decimal_places=2)
    nivel_dificultad = models.CharField(max_length=50)

    def __str__(self):
        return self.nombre_clase

# --- RESERVA CLASE ---
class ReservaClase(models.Model):
    ESTADO_CHOICES = [('Confirmada', 'Confirmada'), ('Pendiente', 'Pendiente'), ('Cancelada', 'Cancelada')]
    socio = models.ForeignKey(Socio, on_delete=models.CASCADE, related_name="reservas")
    clase = models.ForeignKey(Clase, on_delete=models.CASCADE, related_name="reservas")
    fecha_reserva = models.DateTimeField(auto_now_add=True)
    estado_reserva = models.CharField(max_length=50, choices=ESTADO_CHOICES, default='Confirmada')
    fecha_cancelacion = models.DateTimeField(null=True, blank=True)
    comentarios = models.TextField(blank=True, null=True)

    def __str__(self):
        return f"Reserva: {self.socio} - {self.clase}"
    class Meta:
        verbose_name = "Reserva de Clase"
        verbose_name_plural = "Reservas de Clases"

# --- PAGO ---
class Pago(models.Model):
    METODO_PAGO_CHOICES = [('Efectivo', 'Efectivo'), ('Tarjeta', 'Tarjeta de Crédito/Débito'), ('Transferencia', 'Transferencia')]
    socio = models.ForeignKey(Socio, on_delete=models.CASCADE, related_name="pagos")
    fecha_pago = models.DateTimeField(auto_now_add=True)
    monto = models.DecimalField(max_digits=10, decimal_places=2)
    metodo_pago = models.CharField(max_length=50, choices=METODO_PAGO_CHOICES)
    concepto = models.CharField(max_length=100)
    membresia_pagada = models.ForeignKey(Membresia, on_delete=models.SET_NULL, null=True, blank=True)
    estado_pago = models.CharField(max_length=50, default='Pagado')

    def __str__(self):
        return f"Pago #{self.id} - {self.socio} - ${self.monto}"

# --- RUTINA PERSONALIZADA ---
class RutinaPersonalizada(models.Model):
    socio = models.ForeignKey(Socio, on_delete=models.CASCADE, related_name="rutinas")
    entrenador = models.ForeignKey(Entrenador, on_delete=models.SET_NULL, null=True, related_name="rutinas_asignadas")
    fecha_creacion = models.DateField(auto_now_add=True)
    objetivo = models.CharField(max_length=100)
    descripcion_ejercicios = models.TextField()
    frecuencia = models.CharField(max_length=50, help_text="Ej: 3 veces por semana")
    duracion_semanas = models.IntegerField()

    def __str__(self):
        return f"Rutina para {self.socio} - {self.objetivo}"
    class Meta:
        verbose_name = "Rutina Personalizada"
        verbose_name_plural = "Rutinas Personalizadas"
```

**62. Registrar en `members/admin.py`:**
```python
from django.contrib import admin
from .models import Membresia, Socio, Entrenador, Clase, ReservaClase, Pago, RutinaPersonalizada

admin.site.register(Membresia)
admin.site.register(Socio)
admin.site.register(Entrenador)
admin.site.register(Clase)
admin.site.register(ReservaClase)
admin.site.register(Pago)
admin.site.register(RutinaPersonalizada)
```

**13. Migraciones:**
Ejecuta en la terminal:
```bash
python manage.py makemigrations
python manage.py migrate
```

---

### Parte 4: Lógica (Views y URLs)

**14, 24, 30... Views y URLs de la app `members`:**

Crea el archivo `members/urls.py` (si no existe) y agrega todas las rutas:

```python
# members/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('', views.inicio_gimnasio, name='inicio'),

    # Membresia
    path('membresia/agregar/', views.agregar_membresia, name='agregar_membresia'),
    path('membresia/ver/', views.ver_membresias, name='ver_membresias'),
    path('membresia/actualizar/<int:id>/', views.actualizar_membresia, name='actualizar_membresia'),
    path('membresia/actualizar/realizar/<int:id>/', views.realizar_actualizacion_membresia, name='realizar_actualizacion_membresia'),
    path('membresia/borrar/<int:id>/', views.borrar_membresia, name='borrar_membresia'),

    # Socio
    path('socio/agregar/', views.agregar_socio, name='agregar_socio'),
    path('socio/ver/', views.ver_socios, name='ver_socios'),
    path('socio/actualizar/<int:id>/', views.actualizar_socio, name='actualizar_socio'),
    path('socio/actualizar/realizar/<int:id>/', views.realizar_actualizacion_socio, name='realizar_actualizacion_socio'),
    path('socio/borrar/<int:id>/', views.borrar_socio, name='borrar_socio'),

    # Entrenador
    path('entrenador/agregar/', views.agregar_entrenador, name='agregar_entrenador'),
    path('entrenador/ver/', views.ver_entrenadores, name='ver_entrenadores'),
    path('entrenador/actualizar/<int:id>/', views.actualizar_entrenador, name='actualizar_entrenador'),
    path('entrenador/actualizar/realizar/<int:id>/', views.realizar_actualizacion_entrenador, name='realizar_actualizacion_entrenador'),
    path('entrenador/borrar/<int:id>/', views.borrar_entrenador, name='borrar_entrenador'),

    # Clase
    path('clase/agregar/', views.agregar_clase, name='agregar_clase'),
    path('clase/ver/', views.ver_clases, name='ver_clases'),
    path('clase/actualizar/<int:id>/', views.actualizar_clase, name='actualizar_clase'),
    path('clase/actualizar/realizar/<int:id>/', views.realizar_actualizacion_clase, name='realizar_actualizacion_clase'),
    path('clase/borrar/<int:id>/', views.borrar_clase, name='borrar_clase'),
    
    # Rutina, Pago, Reserva siguen el mismo patrón...
]
# Nota: Para ahorrar espacio, he puesto los principales. Debes añadir las líneas para Pago, ReservaClase y RutinaPersonalizada siguiendo el mismo patrón.
```

**Edita `members/views.py`:**
Aquí se implementa la lógica CRUD sin `forms.py` (usando `request.POST.get`).

```python
from django.shortcuts import render, redirect, get_object_or_404
from .models import Membresia, Socio, Entrenador, Clase, ReservaClase, Pago, RutinaPersonalizada
from django.utils import timezone

def inicio_gimnasio(request):
    return render(request, 'inicio.html')

# --- MEMBRESIA ---
def agregar_membresia(request):
    if request.method == 'POST':
        tipo = request.POST.get('tipo_membresia')
        desc = request.POST.get('descripcion')
        costo = request.POST.get('costo')
        duracion = request.POST.get('duracion_meses')
        beneficios = request.POST.get('beneficios')
        sesiones = request.POST.get('num_sesiones_incluidas')
        # Checkbox devuelve 'on' si está marcado, o nada.
        activa = True if request.POST.get('es_activa') else False
        
        Membresia.objects.create(
            tipo_membresia=tipo, descripcion=desc, costo=costo,
            duracion_meses=duracion, beneficios=beneficios,
            num_sesiones_incluidas=sesiones, es_activa=activa
        )
        return redirect('ver_membresias')
    return render(request, 'membresia/agregar_membresia.html')

def ver_membresias(request):
    membresias = Membresia.objects.all()
    return render(request, 'membresia/ver_membresias.html', {'membresias': membresias})

def actualizar_membresia(request, id):
    membresia = get_object_or_404(Membresia, id=id)
    return render(request, 'membresia/actualizar_membresia.html', {'membresia': membresia})

def realizar_actualizacion_membresia(request, id):
    if request.method == 'POST':
        m = get_object_or_404(Membresia, id=id)
        m.tipo_membresia = request.POST.get('tipo_membresia')
        m.descripcion = request.POST.get('descripcion')
        m.costo = request.POST.get('costo')
        m.duracion_meses = request.POST.get('duracion_meses')
        m.beneficios = request.POST.get('beneficios')
        m.num_sesiones_incluidas = request.POST.get('num_sesiones_incluidas')
        m.es_activa = True if request.POST.get('es_activa') else False
        m.save()
        return redirect('ver_membresias')

def borrar_membresia(request, id):
    m = get_object_or_404(Membresia, id=id)
    m.delete()
    return redirect('ver_membresias')

# --- SOCIO (Ejemplo con Llave Foránea) ---
def agregar_socio(request):
    # Necesitamos enviar las membresías para el <select>
    membresias = Membresia.objects.filter(es_activa=True)
    if request.method == 'POST':
        Socio.objects.create(
            nombre=request.POST.get('nombre'),
            apellido=request.POST.get('apellido'),
            fecha_nacimiento=request.POST.get('fecha_nacimiento'),
            genero=request.POST.get('genero'),
            direccion=request.POST.get('direccion'),
            telefono=request.POST.get('telefono'),
            email=request.POST.get('email'),
            membresia_id=request.POST.get('membresia'), # _id para asignar FK directo
            fecha_vencimiento_membresia=request.POST.get('fecha_vencimiento_membresia')
        )
        return redirect('ver_socios')
    return render(request, 'socio/agregar_socio.html', {'membresias': membresias})

def ver_socios(request):
    socios = Socio.objects.all()
    return render(request, 'socio/ver_socios.html', {'socios': socios})

def actualizar_socio(request, id):
    socio = get_object_or_404(Socio, id=id)
    membresias = Membresia.objects.all()
    return render(request, 'socio/actualizar_socio.html', {'socio': socio, 'membresias': membresias})

def realizar_actualizacion_socio(request, id):
    if request.method == 'POST':
        s = get_object_or_404(Socio, id=id)
        s.nombre = request.POST.get('nombre')
        s.apellido = request.POST.get('apellido')
        s.fecha_nacimiento = request.POST.get('fecha_nacimiento')
        s.genero = request.POST.get('genero')
        s.direccion = request.POST.get('direccion')
        s.telefono = request.POST.get('telefono')
        s.email = request.POST.get('email')
        s.membresia_id = request.POST.get('membresia')
        s.fecha_vencimiento_membresia = request.POST.get('fecha_vencimiento_membresia')
        s.save()
        return redirect('ver_socios')

def borrar_socio(request, id):
    s = get_object_or_404(Socio, id=id)
    s.delete()
    return redirect('ver_socios')

# --- ENTRENADOR ---
def agregar_entrenador(request):
    if request.method == 'POST':
        Entrenador.objects.create(
            nombre=request.POST.get('nombre'),
            apellido=request.POST.get('apellido'),
            especialidad=request.POST.get('especialidad'),
            telefono=request.POST.get('telefono'),
            email=request.POST.get('email'),
            fecha_contratacion=request.POST.get('fecha_contratacion'),
            salario=request.POST.get('salario'),
            certificado=request.POST.get('certificado')
        )
        return redirect('ver_entrenadores')
    return render(request, 'entrenador/agregar_entrenador.html')

def ver_entrenadores(request):
    entrenadores = Entrenador.objects.all()
    return render(request, 'entrenador/ver_entrenadores.html', {'entrenadores': entrenadores})

def actualizar_entrenador(request, id):
    entrenador = get_object_or_404(Entrenador, id=id)
    return render(request, 'entrenador/actualizar_entrenador.html', {'entrenador': entrenador})

def realizar_actualizacion_entrenador(request, id):
    if request.method == 'POST':
        e = get_object_or_404(Entrenador, id=id)
        e.nombre = request.POST.get('nombre')
        e.apellido = request.POST.get('apellido')
        e.especialidad = request.POST.get('especialidad')
        e.telefono = request.POST.get('telefono')
        e.email = request.POST.get('email')
        e.fecha_contratacion = request.POST.get('fecha_contratacion')
        e.salario = request.POST.get('salario')
        e.certificado = request.POST.get('certificado')
        e.save()
        return redirect('ver_entrenadores')

def borrar_entrenador(request, id):
    get_object_or_404(Entrenador, id=id).delete()
    return redirect('ver_entrenadores')

# --- CLASE ---
def agregar_clase(request):
    entrenadores = Entrenador.objects.all()
    if request.method == 'POST':
        Clase.objects.create(
            nombre_clase=request.POST.get('nombre_clase'),
            descripcion=request.POST.get('descripcion'),
            horario=request.POST.get('horario'),
            duracion_minutos=request.POST.get('duracion_minutos'),
            entrenador_id=request.POST.get('entrenador'),
            cupo_maximo=request.POST.get('cupo_maximo'),
            costo_clase=request.POST.get('costo_clase'),
            nivel_dificultad=request.POST.get('nivel_dificultad')
        )
        return redirect('ver_clases')
    return render(request, 'clase/agregar_clase.html', {'entrenadores': entrenadores})

def ver_clases(request):
    clases = Clase.objects.all()
    return render(request, 'clase/ver_clases.html', {'clases': clases})

def actualizar_clase(request, id):
    clase = get_object_or_404(Clase, id=id)
    entrenadores = Entrenador.objects.all()
    return render(request, 'clase/actualizar_clase.html', {'clase': clase, 'entrenadores': entrenadores})

def realizar_actualizacion_clase(request, id):
    if request.method == 'POST':
        c = get_object_or_404(Clase, id=id)
        c.nombre_clase = request.POST.get('nombre_clase')
        c.descripcion = request.POST.get('descripcion')
        c.horario = request.POST.get('horario')
        c.duracion_minutos = request.POST.get('duracion_minutos')
        c.entrenador_id = request.POST.get('entrenador')
        c.cupo_maximo = request.POST.get('cupo_maximo')
        c.costo_clase = request.POST.get('costo_clase')
        c.nivel_dificultad = request.POST.get('nivel_dificultad')
        c.save()
        return redirect('ver_clases')

def borrar_clase(request, id):
    get_object_or_404(Clase, id=id).delete()
    return redirect('ver_clases')

# NOTA: Debes replicar esta lógica para ReservaClase, Pago y RutinaPersonalizada.
# La clave es que si el modelo tiene ForeignKey (ej. ReservaClase tiene 'socio' y 'clase'),
# en 'agregar' y 'actualizar' debes pasar las listas (Socio.objects.all(), Clase.objects.all()) al template.
```

---

### Parte 5: Templates (Frontend)

**15. Estructura de carpetas:**
Dentro de `members/`, crea una carpeta `templates`. Dentro de esa, las subcarpetas requeridas:
*   `members/templates/base.html` (y los demás parciales)
*   `members/templates/membresia/`
*   `members/templates/socio/`
*   `members/templates/entrenador/`
*   `members/templates/clase/`
*   `members/templates/reserva_clase/`
*   `members/templates/pago/`
*   `members/templates/rutina_personalizada/`

**17. `members/templates/base.html`:**
```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gym Flame</title>
    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <!-- Iconos de Bootstrap -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.10.0/font/bootstrap-icons.css">
    <style>
        body { background-color: #f8f9fa; color: #333; }
        .navbar { background-color: #ff5722 !important; } /* Color Gym Flame */
        .navbar-brand, .nav-link { color: white !important; }
        footer { background-color: #343a40; color: white; padding: 20px 0; margin-top: 50px; }
        .card { border: none; shadow: 0 4px 8px rgba(0,0,0,0.1); }
    </style>
</head>
<body class="d-flex flex-column min-vh-100">

    {% include 'header.html' %}
    {% include 'navbar.html' %}

    <div class="container mt-4 flex-grow-1">
        {% block content %}
        {% endblock %}
    </div>

    {% include 'footer.html' %}

    <!-- Bootstrap JS -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```

**`members/templates/header.html`:** (Opcional, puede estar vacío o tener un banner)
```html
<header class="bg-dark text-white text-center py-3">
    <h1><i class="bi bi-fire"></i> Gym Flame</h1>
</header>
```

**18. `members/templates/navbar.html`:**
Aquí configuramos el menú con submenús.

```html
<nav class="navbar navbar-expand-lg navbar-dark">
    <div class="container-fluid">
        <a class="navbar-brand" href="{% url 'inicio' %}">Sistema de Administración Gimnasio</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
            <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
            <ul class="navbar-nav ms-auto">
                <li class="nav-item"><a class="nav-link" href="{% url 'inicio' %}"><i class="bi bi-house-door-fill"></i> Inicio</a></li>
                
                <!-- Membresía -->
                <li class="nav-item dropdown">
                    <a class="nav-link dropdown-toggle" href="#" role="button" data-bs-toggle="dropdown"><i class="bi bi-card-checklist"></i> Membresía</a>
                    <ul class="dropdown-menu">
                        <li><a class="dropdown-item" href="{% url 'agregar_membresia' %}">Agregar membresía</a></li>
                        <li><a class="dropdown-item" href="{% url 'ver_membresias' %}">Ver membresía</a></li>
                    </ul>
                </li>

                <!-- Socio -->
                <li class="nav-item dropdown">
                    <a class="nav-link dropdown-toggle" href="#" role="button" data-bs-toggle="dropdown"><i class="bi bi-people-fill"></i> Socio</a>
                    <ul class="dropdown-menu">
                        <li><a class="dropdown-item" href="{% url 'agregar_socio' %}">Agregar socio</a></li>
                        <li><a class="dropdown-item" href="{% url 'ver_socios' %}">Ver socio</a></li>
                    </ul>
                </li>

                <!-- Entrenador -->
                <li class="nav-item dropdown">
                    <a class="nav-link dropdown-toggle" href="#" role="button" data-bs-toggle="dropdown"><i class="bi bi-person-badge-fill"></i> Entrenador</a>
                    <ul class="dropdown-menu">
                        <li><a class="dropdown-item" href="{% url 'agregar_entrenador' %}">Agregar entrenador</a></li>
                        <li><a class="dropdown-item" href="{% url 'ver_entrenadores' %}">Ver entrenadores</a></li>
                    </ul>
                </li>
                
                <!-- Clase -->
                <li class="nav-item dropdown">
                    <a class="nav-link dropdown-toggle" href="#" role="button" data-bs-toggle="dropdown"><i class="bi bi-calendar-event"></i> Clase</a>
                    <ul class="dropdown-menu">
                        <li><a class="dropdown-item" href="{% url 'agregar_clase' %}">Agregar clase</a></li>
                        <li><a class="dropdown-item" href="{% url 'ver_clases' %}">Ver clases</a></li>
                    </ul>
                </li>

                <!-- Reserva Clase, Pago, Rutina (Repetir estructura cambiando URLs e Iconos) -->
                 <li class="nav-item dropdown">
                    <a class="nav-link dropdown-toggle" href="#" role="button" data-bs-toggle="dropdown"><i class="bi bi-bookmark-check"></i> Reservas</a>
                    <ul class="dropdown-menu">
                        <li><a class="dropdown-item" href="#">Ver reservas (Configurar URL)</a></li>
                    </ul>
                </li>
            </ul>
        </div>
    </div>
</nav>
```

**19. `members/templates/footer.html`:**
```html
<footer class="text-center">
    <div class="container">
        <p>&copy; {% now "Y" %} Gym Flame. Todos los derechos reservados.</p>
        <p class="mb-0">Creado por Jesus Gael Carrasco Avitia, Cbtis 128</p>
    </div>
</footer>
```

**20. `members/templates/inicio.html`:**
```html
{% extends 'base.html' %}
{% block content %}
<div class="text-center">
    <h2 class="display-4 mb-4">Bienvenido a Gym Flame</h2>
    <p class="lead">El sistema más completo para gestionar tu entrenamiento.</p>
    <img src="https://images.unsplash.com/photo-1534438327276-14e5300c3a48?ixlib=rb-4.0.3&auto=format&fit=crop&w=1470&q=80" 
         alt="Gimnasio" class="img-fluid rounded shadow" style="max-height: 500px; width: 100%; object-fit: cover;">
</div>
{% endblock %}
```

---

### Parte 6: Templates CRUD (Ejemplos Completos)

#### A. Membresía (Sin llaves foráneas)

**22. `members/templates/membresia/agregar_membresia.html`:**
```html
{% extends 'base.html' %}
{% block content %}
<div class="card p-4">
    <h3>Agregar Membresía</h3>
    <form method="POST">
        {% csrf_token %}
        <div class="mb-3"><label>Tipo:</label><input type="text" name="tipo_membresia" class="form-control" required></div>
        <div class="mb-3"><label>Descripción:</label><textarea name="descripcion" class="form-control" required></textarea></div>
        <div class="mb-3"><label>Costo:</label><input type="number" step="0.01" name="costo" class="form-control" required></div>
        <div class="mb-3"><label>Duración (Meses):</label><input type="number" name="duracion_meses" class="form-control" required></div>
        <div class="mb-3"><label>Beneficios:</label><textarea name="beneficios" class="form-control" required></textarea></div>
        <div class="mb-3"><label>Sesiones Incluidas:</label><input type="number" name="num_sesiones_incluidas" class="form-control" required></div>
        <div class="mb-3 form-check">
            <input type="checkbox" name="es_activa" class="form-check-input" checked>
            <label class="form-check-label">¿Activa?</label>
        </div>
        <button type="submit" class="btn btn-success"><i class="bi bi-save"></i> Guardar</button>
    </form>
</div>
{% endblock %}
```

**`members/templates/membresia/ver_membresias.html`:**
```html
{% extends 'base.html' %}
{% block content %}
<h3>Lista de Membresías</h3>
<a href="{% url 'agregar_membresia' %}" class="btn btn-primary mb-3"><i class="bi bi-plus-circle"></i> Agregar</a>
<table class="table table-striped table-hover">
    <thead class="table-dark">
        <tr>
            <th>Tipo</th>
            <th>Costo</th>
            <th>Duración</th>
            <th>Acciones</th>
        </tr>
    </thead>
    <tbody>
        {% for m in membresias %}
        <tr>
            <td>{{ m.tipo_membresia }}</td>
            <td>${{ m.costo }}</td>
            <td>{{ m.duracion_meses }} meses</td>
            <td>
                <!-- El botón 'Ver' podría ir a actualizar o a un detalle separado, aquí usamos actualizar para simplificar -->
                <a href="{% url 'actualizar_membresia' m.id %}" class="btn btn-info btn-sm"><i class="bi bi-eye"></i> Ver/Editar</a>
                <a href="{% url 'borrar_membresia' m.id %}" class="btn btn-danger btn-sm" onclick="return confirm('¿Eliminar?');"><i class="bi bi-trash"></i> Borrar</a>
            </td>
        </tr>
        {% endfor %}
    </tbody>
</table>
{% endblock %}
```

**`members/templates/membresia/actualizar_membresia.html`:**
Es similar a agregar, pero con `value="{{ membresia.campo }}"` y apuntando a la URL de `realizar_actualizacion`.
```html
{% extends 'base.html' %}
{% block content %}
<div class="card p-4">
    <h3>Actualizar Membresía</h3>
    <form action="{% url 'realizar_actualizacion_membresia' membresia.id %}" method="POST">
        {% csrf_token %}
        <div class="mb-3"><label>Tipo:</label><input type="text" name="tipo_membresia" value="{{ membresia.tipo_membresia }}" class="form-control"></div>
        <div class="mb-3"><label>Descripción:</label><textarea name="descripcion" class="form-control">{{ membresia.descripcion }}</textarea></div>
        <div class="mb-3"><label>Costo:</label><input type="number" step="0.01" name="costo" value="{{ membresia.costo }}" class="form-control"></div>
        <div class="mb-3"><label>Duración:</label><input type="number" name="duracion_meses" value="{{ membresia.duracion_meses }}" class="form-control"></div>
        <div class="mb-3"><label>Beneficios:</label><textarea name="beneficios" class="form-control">{{ membresia.beneficios }}</textarea></div>
        <div class="mb-3"><label>Sesiones:</label><input type="number" name="num_sesiones_incluidas" value="{{ membresia.num_sesiones_incluidas }}" class="form-control"></div>
        <div class="mb-3 form-check">
            <input type="checkbox" name="es_activa" class="form-check-input" {% if membresia.es_activa %}checked{% endif %}>
            <label class="form-check-label">¿Activa?</label>
        </div>
        <button type="submit" class="btn btn-warning"><i class="bi bi-pencil"></i> Actualizar</button>
    </form>
</div>
{% endblock %}
```

#### B. Socio (Con LLave Foránea - Select)

**28. `members/templates/socio/agregar_socio.html`:**
```html
{% extends 'base.html' %}
{% block content %}
<div class="card p-4">
    <h3>Agregar Socio</h3>
    <form method="POST">
        {% csrf_token %}
        <div class="row">
            <div class="col-md-6 mb-3"><label>Nombre:</label><input type="text" name="nombre" class="form-control"></div>
            <div class="col-md-6 mb-3"><label>Apellido:</label><input type="text" name="apellido" class="form-control"></div>
        </div>
        <div class="mb-3"><label>Fecha Nacimiento:</label><input type="date" name="fecha_nacimiento" class="form-control"></div>
        <div class="mb-3"><label>Género:</label>
            <select name="genero" class="form-select">
                <option value="M">Masculino</option>
                <option value="F">Femenino</option>
                <option value="O">Otro</option>
            </select>
        </div>
        <div class="mb-3"><label>Dirección:</label><input type="text" name="direccion" class="form-control"></div>
        <div class="mb-3"><label>Teléfono:</label><input type="text" name="telefono" class="form-control"></div>
        <div class="mb-3"><label>Email:</label><input type="email" name="email" class="form-control"></div>
        
        <!-- LLAVE FORÁNEA -->
        <div class="mb-3"><label>Membresía:</label>
            <select name="membresia" class="form-select">
                {% for m in membresias %}
                    <option value="{{ m.id }}">{{ m.tipo_membresia }} - ${{ m.costo }}</option>
                {% endfor %}
            </select>
        </div>
        
        <div class="mb-3"><label>Vencimiento Membresía:</label><input type="date" name="fecha_vencimiento_membresia" class="form-control"></div>
        <button type="submit" class="btn btn-success">Guardar</button>
    </form>
</div>
{% endblock %}
```

**`members/templates/socio/ver_socios.html`:**
```html
{% extends 'base.html' %}
{% block content %}
<h3>Socios Registrados</h3>
<a href="{% url 'agregar_socio' %}" class="btn btn-primary mb-3">Agregar</a>
<table class="table table-striped">
    <thead class="table-dark">
        <tr>
            <th>Nombre Completo</th>
            <th>Teléfono</th>
            <th>Membresía</th>
            <th>Vencimiento</th>
            <th>Acciones</th>
        </tr>
    </thead>
    <tbody>
        {% for s in socios %}
        <tr>
            <td>{{ s.nombre }} {{ s.apellido }}</td>
            <td>{{ s.telefono }}</td>
            <td>{{ s.membresia.tipo_membresia }}</td>
            <td>{{ s.fecha_vencimiento_membresia }}</td>
            <td>
                <a href="{% url 'actualizar_socio' s.id %}" class="btn btn-info btn-sm">Editar</a>
                <a href="{% url 'borrar_socio' s.id %}" class="btn btn-danger btn-sm" onclick="return confirm('¿Eliminar?');">Borrar</a>
            </td>
        </tr>
        {% endfor %}
    </tbody>
</table>
{% endblock %}
```

Claro que sí. Aquí tienes **todos los pasos restantes** detallados (del 33 al 61) para completar los módulos de Entrenador, Clase, Reserva de Clase, Pago y Rutina Personalizada.

---

### Paso 1: Completar `members/urls.py` (Pasos 36, 41, 47, 53, 59)

Abre el archivo `members/urls.py` y asegúrate de que tenga **todas** estas rutas. Copia y pega para reemplazar o completar lo que tenías:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.inicio_gimnasio, name='inicio'),

    # --- MEMBRESIA ---
    path('membresia/agregar/', views.agregar_membresia, name='agregar_membresia'),
    path('membresia/ver/', views.ver_membresias, name='ver_membresias'),
    path('membresia/actualizar/<int:id>/', views.actualizar_membresia, name='actualizar_membresia'),
    path('membresia/actualizar/realizar/<int:id>/', views.realizar_actualizacion_membresia, name='realizar_actualizacion_membresia'),
    path('membresia/borrar/<int:id>/', views.borrar_membresia, name='borrar_membresia'),

    # --- SOCIO ---
    path('socio/agregar/', views.agregar_socio, name='agregar_socio'),
    path('socio/ver/', views.ver_socios, name='ver_socios'),
    path('socio/actualizar/<int:id>/', views.actualizar_socio, name='actualizar_socio'),
    path('socio/actualizar/realizar/<int:id>/', views.realizar_actualizacion_socio, name='realizar_actualizacion_socio'),
    path('socio/borrar/<int:id>/', views.borrar_socio, name='borrar_socio'),

    # --- ENTRENADOR ---
    path('entrenador/agregar/', views.agregar_entrenador, name='agregar_entrenador'),
    path('entrenador/ver/', views.ver_entrenadores, name='ver_entrenadores'),
    path('entrenador/actualizar/<int:id>/', views.actualizar_entrenador, name='actualizar_entrenador'),
    path('entrenador/actualizar/realizar/<int:id>/', views.realizar_actualizacion_entrenador, name='realizar_actualizacion_entrenador'),
    path('entrenador/borrar/<int:id>/', views.borrar_entrenador, name='borrar_entrenador'),

    # --- CLASE ---
    path('clase/agregar/', views.agregar_clase, name='agregar_clase'),
    path('clase/ver/', views.ver_clases, name='ver_clases'),
    path('clase/actualizar/<int:id>/', views.actualizar_clase, name='actualizar_clase'),
    path('clase/actualizar/realizar/<int:id>/', views.realizar_actualizacion_clase, name='realizar_actualizacion_clase'),
    path('clase/borrar/<int:id>/', views.borrar_clase, name='borrar_clase'),

    # --- RESERVA CLASE ---
    path('reserva/agregar/', views.agregar_reserva_clase, name='agregar_reserva_clase'),
    path('reserva/ver/', views.ver_reservas_clase, name='ver_reservas_clase'),
    path('reserva/actualizar/<int:id>/', views.actualizar_reserva_clase, name='actualizar_reserva_clase'),
    path('reserva/actualizar/realizar/<int:id>/', views.realizar_actualizacion_reserva_clase, name='realizar_actualizacion_reserva_clase'),
    path('reserva/borrar/<int:id>/', views.borrar_reserva_clase, name='borrar_reserva_clase'),

    # --- PAGO ---
    path('pago/agregar/', views.agregar_pago, name='agregar_pago'),
    path('pago/ver/', views.ver_pagos, name='ver_pagos'),
    path('pago/actualizar/<int:id>/', views.actualizar_pago, name='actualizar_pago'),
    path('pago/actualizar/realizar/<int:id>/', views.realizar_actualizacion_pago, name='realizar_actualizacion_pago'),
    path('pago/borrar/<int:id>/', views.borrar_pago, name='borrar_pago'),

    # --- RUTINA PERSONALIZADA ---
    path('rutina/agregar/', views.agregar_rutina_personalizada, name='agregar_rutina_personalizada'),
    path('rutina/ver/', views.ver_rutinas_personalizadas, name='ver_rutinas_personalizadas'),
    path('rutina/actualizar/<int:id>/', views.actualizar_rutina_personalizada, name='actualizar_rutina_personalizada'),
    path('rutina/actualizar/realizar/<int:id>/', views.realizar_actualizacion_rutina_personalizada, name='realizar_actualizacion_rutina_personalizada'),
    path('rutina/borrar/<int:id>/', views.borrar_rutina_personalizada, name='borrar_rutina_personalizada'),
]
```

---

### Paso 2: Completar `members/views.py`

Agrega el código faltante para los modelos restantes. Asegúrate de importar todos los modelos al inicio del archivo:

```python
# Asegúrate de tener esto al inicio
from django.shortcuts import render, redirect, get_object_or_404
from .models import Membresia, Socio, Entrenador, Clase, ReservaClase, Pago, RutinaPersonalizada

# ... (Aquí va el código de Inicio, Membresia, Socio, Entrenador y Clase que te di antes) ...

# --- RESERVA CLASE ---
def agregar_reserva_clase(request):
    socios = Socio.objects.all()
    clases = Clase.objects.all()
    if request.method == 'POST':
        ReservaClase.objects.create(
            socio_id=request.POST.get('socio'),
            clase_id=request.POST.get('clase'),
            estado_reserva=request.POST.get('estado_reserva'),
            comentarios=request.POST.get('comentarios')
        )
        return redirect('ver_reservas_clase')
    return render(request, 'reserva_clase/agregar_reserva_clase.html', {'socios': socios, 'clases': clases})

def ver_reservas_clase(request):
    reservas = ReservaClase.objects.all()
    return render(request, 'reserva_clase/ver_reservas_clase.html', {'reservas': reservas})

def actualizar_reserva_clase(request, id):
    reserva = get_object_or_404(ReservaClase, id=id)
    socios = Socio.objects.all()
    clases = Clase.objects.all()
    return render(request, 'reserva_clase/actualizar_reserva_clase.html', {'reserva': reserva, 'socios': socios, 'clases': clases})

def realizar_actualizacion_reserva_clase(request, id):
    if request.method == 'POST':
        r = get_object_or_404(ReservaClase, id=id)
        r.socio_id = request.POST.get('socio')
        r.clase_id = request.POST.get('clase')
        r.estado_reserva = request.POST.get('estado_reserva')
        r.comentarios = request.POST.get('comentarios')
        r.save()
        return redirect('ver_reservas_clase')

def borrar_reserva_clase(request, id):
    get_object_or_404(ReservaClase, id=id).delete()
    return redirect('ver_reservas_clase')

# --- PAGO ---
def agregar_pago(request):
    socios = Socio.objects.all()
    membresias = Membresia.objects.all()
    if request.method == 'POST':
        Pago.objects.create(
            socio_id=request.POST.get('socio'),
            monto=request.POST.get('monto'),
            metodo_pago=request.POST.get('metodo_pago'),
            concepto=request.POST.get('concepto'),
            membresia_pagada_id=request.POST.get('membresia_pagada'),
            estado_pago=request.POST.get('estado_pago')
        )
        return redirect('ver_pagos')
    return render(request, 'pago/agregar_pago.html', {'socios': socios, 'membresias': membresias})

def ver_pagos(request):
    pagos = Pago.objects.all()
    return render(request, 'pago/ver_pagos.html', {'pagos': pagos})

def actualizar_pago(request, id):
    pago = get_object_or_404(Pago, id=id)
    socios = Socio.objects.all()
    membresias = Membresia.objects.all()
    return render(request, 'pago/actualizar_pago.html', {'pago': pago, 'socios': socios, 'membresias': membresias})

def realizar_actualizacion_pago(request, id):
    if request.method == 'POST':
        p = get_object_or_404(Pago, id=id)
        p.socio_id = request.POST.get('socio')
        p.monto = request.POST.get('monto')
        p.metodo_pago = request.POST.get('metodo_pago')
        p.concepto = request.POST.get('concepto')
        p.membresia_pagada_id = request.POST.get('membresia_pagada')
        p.estado_pago = request.POST.get('estado_pago')
        p.save()
        return redirect('ver_pagos')

def borrar_pago(request, id):
    get_object_or_404(Pago, id=id).delete()
    return redirect('ver_pagos')

# --- RUTINA PERSONALIZADA ---
def agregar_rutina_personalizada(request):
    socios = Socio.objects.all()
    entrenadores = Entrenador.objects.all()
    if request.method == 'POST':
        RutinaPersonalizada.objects.create(
            socio_id=request.POST.get('socio'),
            entrenador_id=request.POST.get('entrenador'),
            objetivo=request.POST.get('objetivo'),
            descripcion_ejercicios=request.POST.get('descripcion_ejercicios'),
            frecuencia=request.POST.get('frecuencia'),
            duracion_semanas=request.POST.get('duracion_semanas')
        )
        return redirect('ver_rutinas_personalizadas')
    return render(request, 'rutina_personalizada/agregar_rutina_personalizada.html', {'socios': socios, 'entrenadores': entrenadores})

def ver_rutinas_personalizadas(request):
    rutinas = RutinaPersonalizada.objects.all()
    return render(request, 'rutina_personalizada/ver_rutinas_personalizadas.html', {'rutinas': rutinas})

def actualizar_rutina_personalizada(request, id):
    rutina = get_object_or_404(RutinaPersonalizada, id=id)
    socios = Socio.objects.all()
    entrenadores = Entrenador.objects.all()
    return render(request, 'rutina_personalizada/actualizar_rutina_personalizada.html', {'rutina': rutina, 'socios': socios, 'entrenadores': entrenadores})

def realizar_actualizacion_rutina_personalizada(request, id):
    if request.method == 'POST':
        r = get_object_or_404(RutinaPersonalizada, id=id)
        r.socio_id = request.POST.get('socio')
        r.entrenador_id = request.POST.get('entrenador')
        r.objetivo = request.POST.get('objetivo')
        r.descripcion_ejercicios = request.POST.get('descripcion_ejercicios')
        r.frecuencia = request.POST.get('frecuencia')
        r.duracion_semanas = request.POST.get('duracion_semanas')
        r.save()
        return redirect('ver_rutinas_personalizadas')

def borrar_rutina_personalizada(request, id):
    get_object_or_404(RutinaPersonalizada, id=id).delete()
    return redirect('ver_rutinas_personalizadas')
```

---

### Paso 3: Templates restantes (HTML)

Crea las carpetas y archivos indicados a continuación.

#### 3.1 Entrenador (Pasos 33, 34)
Carpeta: `members/templates/entrenador/`

**agregar_entrenador.html**
```html
{% extends 'base.html' %}
{% block content %}
<div class="card p-4">
    <h3>Agregar Entrenador</h3>
    <form method="POST">
        {% csrf_token %}
        <div class="mb-3"><label>Nombre:</label><input type="text" name="nombre" class="form-control" required></div>
        <div class="mb-3"><label>Apellido:</label><input type="text" name="apellido" class="form-control" required></div>
        <div class="mb-3"><label>Especialidad:</label><input type="text" name="especialidad" class="form-control" required></div>
        <div class="mb-3"><label>Teléfono:</label><input type="text" name="telefono" class="form-control" required></div>
        <div class="mb-3"><label>Email:</label><input type="email" name="email" class="form-control" required></div>
        <div class="mb-3"><label>Fecha Contratación:</label><input type="date" name="fecha_contratacion" class="form-control" required></div>
        <div class="mb-3"><label>Salario:</label><input type="number" step="0.01" name="salario" class="form-control" required></div>
        <div class="mb-3"><label>Certificado:</label><input type="text" name="certificado" class="form-control" required></div>
        <button type="submit" class="btn btn-success">Guardar</button>
    </form>
</div>
{% endblock %}
```

**ver_entrenadores.html**
```html
{% extends 'base.html' %}
{% block content %}
<h3>Entrenadores</h3>
<a href="{% url 'agregar_entrenador' %}" class="btn btn-primary mb-3">Agregar</a>
<table class="table table-striped">
    <thead class="table-dark">
        <tr><th>Nombre</th><th>Especialidad</th><th>Email</th><th>Acciones</th></tr>
    </thead>
    <tbody>
        {% for e in entrenadores %}
        <tr>
            <td>{{ e.nombre }} {{ e.apellido }}</td>
            <td>{{ e.especialidad }}</td>
            <td>{{ e.email }}</td>
            <td>
                <a href="{% url 'actualizar_entrenador' e.id %}" class="btn btn-info btn-sm">Editar</a>
                <a href="{% url 'borrar_entrenador' e.id %}" class="btn btn-danger btn-sm" onclick="return confirm('¿Eliminar?');">Borrar</a>
            </td>
        </tr>
        {% endfor %}
    </tbody>
</table>
{% endblock %}
```

**actualizar_entrenador.html**
```html
{% extends 'base.html' %}
{% block content %}
<div class="card p-4">
    <h3>Actualizar Entrenador</h3>
    <form action="{% url 'realizar_actualizacion_entrenador' entrenador.id %}" method="POST">
        {% csrf_token %}
        <div class="mb-3"><label>Nombre:</label><input type="text" name="nombre" value="{{ entrenador.nombre }}" class="form-control"></div>
        <div class="mb-3"><label>Apellido:</label><input type="text" name="apellido" value="{{ entrenador.apellido }}" class="form-control"></div>
        <div class="mb-3"><label>Especialidad:</label><input type="text" name="especialidad" value="{{ entrenador.especialidad }}" class="form-control"></div>
        <div class="mb-3"><label>Teléfono:</label><input type="text" name="telefono" value="{{ entrenador.telefono }}" class="form-control"></div>
        <div class="mb-3"><label>Email:</label><input type="email" name="email" value="{{ entrenador.email }}" class="form-control"></div>
        <div class="mb-3"><label>Fecha Contratación:</label><input type="date" name="fecha_contratacion" value="{{ entrenador.fecha_contratacion|date:'Y-m-d' }}" class="form-control"></div>
        <div class="mb-3"><label>Salario:</label><input type="number" step="0.01" name="salario" value="{{ entrenador.salario|stringformat:'.2f' }}" class="form-control"></div>
        <div class="mb-3"><label>Certificado:</label><input type="text" name="certificado" value="{{ entrenador.certificado }}" class="form-control"></div>
        <button type="submit" class="btn btn-warning">Actualizar</button>
    </form>
</div>
{% endblock %}
```

#### 3.2 Clase (Pasos 38, 39)
Carpeta: `members/templates/clase/`

**agregar_clase.html**
```html
{% extends 'base.html' %}
{% block content %}
<div class="card p-4">
    <h3>Agregar Clase</h3>
    <form method="POST">
        {% csrf_token %}
        <div class="mb-3"><label>Nombre Clase:</label><input type="text" name="nombre_clase" class="form-control"></div>
        <div class="mb-3"><label>Descripción:</label><textarea name="descripcion" class="form-control"></textarea></div>
        <div class="mb-3"><label>Horario:</label><input type="text" name="horario" class="form-control"></div>
        <div class="mb-3"><label>Duración (min):</label><input type="number" name="duracion_minutos" class="form-control"></div>
        <div class="mb-3"><label>Entrenador:</label>
            <select name="entrenador" class="form-select">
                {% for e in entrenadores %}
                <option value="{{ e.id }}">{{ e.nombre }} {{ e.apellido }}</option>
                {% endfor %}
            </select>
        </div>
        <div class="mb-3"><label>Cupo Máximo:</label><input type="number" name="cupo_maximo" class="form-control"></div>
        <div class="mb-3"><label>Costo:</label><input type="number" step="0.01" name="costo_clase" class="form-control"></div>
        <div class="mb-3"><label>Dificultad:</label><input type="text" name="nivel_dificultad" class="form-control"></div>
        <button type="submit" class="btn btn-success">Guardar</button>
    </form>
</div>
{% endblock %}
```

**ver_clases.html**
```html
{% extends 'base.html' %}
{% block content %}
<h3>Clases</h3>
<a href="{% url 'agregar_clase' %}" class="btn btn-primary mb-3">Agregar</a>
<table class="table table-striped">
    <thead class="table-dark">
        <tr><th>Clase</th><th>Horario</th><th>Entrenador</th><th>Acciones</th></tr>
    </thead>
    <tbody>
        {% for c in clases %}
        <tr>
            <td>{{ c.nombre_clase }}</td>
            <td>{{ c.horario }}</td>
            <td>{{ c.entrenador }}</td>
            <td>
                <a href="{% url 'actualizar_clase' c.id %}" class="btn btn-info btn-sm">Editar</a>
                <a href="{% url 'borrar_clase' c.id %}" class="btn btn-danger btn-sm" onclick="return confirm('¿Eliminar?');">Borrar</a>
            </td>
        </tr>
        {% endfor %}
    </tbody>
</table>
{% endblock %}
```

**actualizar_clase.html**
```html
{% extends 'base.html' %}
{% block content %}
<div class="card p-4">
    <h3>Actualizar Clase</h3>
    <form action="{% url 'realizar_actualizacion_clase' clase.id %}" method="POST">
        {% csrf_token %}
        <div class="mb-3"><label>Nombre:</label><input type="text" name="nombre_clase" value="{{ clase.nombre_clase }}" class="form-control"></div>
        <div class="mb-3"><label>Descripción:</label><textarea name="descripcion" class="form-control">{{ clase.descripcion }}</textarea></div>
        <div class="mb-3"><label>Horario:</label><input type="text" name="horario" value="{{ clase.horario }}" class="form-control"></div>
        <div class="mb-3"><label>Duración:</label><input type="number" name="duracion_minutos" value="{{ clase.duracion_minutos }}" class="form-control"></div>
        <div class="mb-3"><label>Entrenador:</label>
            <select name="entrenador" class="form-select">
                {% for e in entrenadores %}
                <option value="{{ e.id }}" {% if clase.entrenador.id == e.id %}selected{% endif %}>{{ e.nombre }} {{ e.apellido }}</option>
                {% endfor %}
            </select>
        </div>
        <div class="mb-3"><label>Cupo:</label><input type="number" name="cupo_maximo" value="{{ clase.cupo_maximo }}" class="form-control"></div>
        <div class="mb-3"><label>Costo:</label><input type="number" step="0.01" name="costo_clase" value="{{ clase.costo_clase }}" class="form-control"></div>
        <div class="mb-3"><label>Dificultad:</label><input type="text" name="nivel_dificultad" value="{{ clase.nivel_dificultad }}" class="form-control"></div>
        <button type="submit" class="btn btn-warning">Actualizar</button>
    </form>
</div>
{% endblock %}
```

#### 3.3 Reserva Clase (Pasos 44, 45)
Carpeta: `members/templates/reserva_clase/`

**agregar_reserva_clase.html**
```html
{% extends 'base.html' %}
{% block content %}
<div class="card p-4">
    <h3>Nueva Reserva</h3>
    <form method="POST">
        {% csrf_token %}
        <div class="mb-3"><label>Socio:</label>
            <select name="socio" class="form-select">
                {% for s in socios %}
                <option value="{{ s.id }}">{{ s.nombre }} {{ s.apellido }}</option>
                {% endfor %}
            </select>
        </div>
        <div class="mb-3"><label>Clase:</label>
            <select name="clase" class="form-select">
                {% for c in clases %}
                <option value="{{ c.id }}">{{ c.nombre_clase }} ({{ c.horario }})</option>
                {% endfor %}
            </select>
        </div>
        <div class="mb-3"><label>Estado:</label>
            <select name="estado_reserva" class="form-select">
                <option value="Confirmada">Confirmada</option>
                <option value="Pendiente">Pendiente</option>
                <option value="Cancelada">Cancelada</option>
            </select>
        </div>
        <div class="mb-3"><label>Comentarios:</label><textarea name="comentarios" class="form-control"></textarea></div>
        <button type="submit" class="btn btn-success">Guardar</button>
    </form>
</div>
{% endblock %}
```

**ver_reservas_clase.html**
```html
{% extends 'base.html' %}
{% block content %}
<h3>Reservas de Clases</h3>
<a href="{% url 'agregar_reserva_clase' %}" class="btn btn-primary mb-3">Agregar</a>
<table class="table table-striped">
    <thead class="table-dark">
        <tr><th>Socio</th><th>Clase</th><th>Estado</th><th>Acciones</th></tr>
    </thead>
    <tbody>
        {% for r in reservas %}
        <tr>
            <td>{{ r.socio }}</td>
            <td>{{ r.clase }}</td>
            <td>{{ r.estado_reserva }}</td>
            <td>
                <a href="{% url 'actualizar_reserva_clase' r.id %}" class="btn btn-info btn-sm">Editar</a>
                <a href="{% url 'borrar_reserva_clase' r.id %}" class="btn btn-danger btn-sm" onclick="return confirm('¿Eliminar?');">Borrar</a>
            </td>
        </tr>
        {% endfor %}
    </tbody>
</table>
{% endblock %}
```

**actualizar_reserva_clase.html**
```html
{% extends 'base.html' %}
{% block content %}
<div class="card p-4">
    <h3>Actualizar Reserva</h3>
    <form action="{% url 'realizar_actualizacion_reserva_clase' reserva.id %}" method="POST">
        {% csrf_token %}
        <div class="mb-3"><label>Socio:</label>
            <select name="socio" class="form-select">
                {% for s in socios %}
                <option value="{{ s.id }}" {% if reserva.socio.id == s.id %}selected{% endif %}>{{ s.nombre }} {{ s.apellido }}</option>
                {% endfor %}
            </select>
        </div>
        <div class="mb-3"><label>Clase:</label>
            <select name="clase" class="form-select">
                {% for c in clases %}
                <option value="{{ c.id }}" {% if reserva.clase.id == c.id %}selected{% endif %}>{{ c.nombre_clase }}</option>
                {% endfor %}
            </select>
        </div>
        <div class="mb-3"><label>Estado:</label>
            <select name="estado_reserva" class="form-select">
                <option value="Confirmada" {% if reserva.estado_reserva == 'Confirmada' %}selected{% endif %}>Confirmada</option>
                <option value="Pendiente" {% if reserva.estado_reserva == 'Pendiente' %}selected{% endif %}>Pendiente</option>
                <option value="Cancelada" {% if reserva.estado_reserva == 'Cancelada' %}selected{% endif %}>Cancelada</option>
            </select>
        </div>
        <div class="mb-3"><label>Comentarios:</label><textarea name="comentarios" class="form-control">{{ reserva.comentarios }}</textarea></div>
        <button type="submit" class="btn btn-warning">Actualizar</button>
    </form>
</div>
{% endblock %}
```

#### 3.4 Pago (Pasos 50, 51)
Carpeta: `members/templates/pago/`

**agregar_pago.html**
```html
{% extends 'base.html' %}
{% block content %}
<div class="card p-4">
    <h3>Registrar Pago</h3>
    <form method="POST">
        {% csrf_token %}
        <div class="mb-3"><label>Socio:</label>
            <select name="socio" class="form-select">
                {% for s in socios %}
                <option value="{{ s.id }}">{{ s.nombre }} {{ s.apellido }}</option>
                {% endfor %}
            </select>
        </div>
        <div class="mb-3"><label>Monto:</label><input type="number" step="0.01" name="monto" class="form-control"></div>
        <div class="mb-3"><label>Método de Pago:</label>
            <select name="metodo_pago" class="form-select">
                <option value="Efectivo">Efectivo</option>
                <option value="Tarjeta">Tarjeta</option>
                <option value="Transferencia">Transferencia</option>
            </select>
        </div>
        <div class="mb-3"><label>Concepto:</label><input type="text" name="concepto" class="form-control"></div>
        <div class="mb-3"><label>Membresía Pagada (Opcional):</label>
            <select name="membresia_pagada" class="form-select">
                <option value="">-- Ninguna --</option>
                {% for m in membresias %}
                <option value="{{ m.id }}">{{ m.tipo_membresia }}</option>
                {% endfor %}
            </select>
        </div>
        <div class="mb-3"><label>Estado:</label><input type="text" name="estado_pago" value="Pagado" class="form-control"></div>
        <button type="submit" class="btn btn-success">Guardar</button>
    </form>
</div>
{% endblock %}
```

**ver_pagos.html**
```html
{% extends 'base.html' %}
{% block content %}
<h3>Pagos Registrados</h3>
<a href="{% url 'agregar_pago' %}" class="btn btn-primary mb-3">Agregar</a>
<table class="table table-striped">
    <thead class="table-dark">
        <tr><th>Socio</th><th>Monto</th><th>Método</th><th>Concepto</th><th>Acciones</th></tr>
    </thead>
    <tbody>
        {% for p in pagos %}
        <tr>
            <td>{{ p.socio }}</td>
            <td>${{ p.monto }}</td>
            <td>{{ p.metodo_pago }}</td>
            <td>{{ p.concepto }}</td>
            <td>
                <a href="{% url 'actualizar_pago' p.id %}" class="btn btn-info btn-sm">Editar</a>
                <a href="{% url 'borrar_pago' p.id %}" class="btn btn-danger btn-sm" onclick="return confirm('¿Eliminar?');">Borrar</a>
            </td>
        </tr>
        {% endfor %}
    </tbody>
</table>
{% endblock %}
```

**actualizar_pago.html**
```html
{% extends 'base.html' %}
{% block content %}
<div class="card p-4">
    <h3>Actualizar Pago</h3>
    <form action="{% url 'realizar_actualizacion_pago' pago.id %}" method="POST">
        {% csrf_token %}
        <div class="mb-3"><label>Socio:</label>
            <select name="socio" class="form-select">
                {% for s in socios %}
                <option value="{{ s.id }}" {% if pago.socio.id == s.id %}selected{% endif %}>{{ s.nombre }} {{ s.apellido }}</option>
                {% endfor %}
            </select>
        </div>
        <div class="mb-3"><label>Monto:</label><input type="number" step="0.01" name="monto" value="{{ pago.monto|stringformat:'.2f' }}" class="form-control"></div>
        <div class="mb-3"><label>Método de Pago:</label>
            <select name="metodo_pago" class="form-select">
                <option value="Efectivo" {% if pago.metodo_pago == 'Efectivo' %}selected{% endif %}>Efectivo</option>
                <option value="Tarjeta" {% if pago.metodo_pago == 'Tarjeta' %}selected{% endif %}>Tarjeta</option>
                <option value="Transferencia" {% if pago.metodo_pago == 'Transferencia' %}selected{% endif %}>Transferencia</option>
            </select>
        </div>
        <div class="mb-3"><label>Concepto:</label><input type="text" name="concepto" value="{{ pago.concepto }}" class="form-control"></div>
        <div class="mb-3"><label>Membresía Pagada:</label>
            <select name="membresia_pagada" class="form-select">
                <option value="">-- Ninguna --</option>
                {% for m in membresias %}
                <option value="{{ m.id }}" {% if pago.membresia_pagada.id == m.id %}selected{% endif %}>{{ m.tipo_membresia }}</option>
                {% endfor %}
            </select>
        </div>
        <div class="mb-3"><label>Estado:</label><input type="text" name="estado_pago" value="{{ pago.estado_pago }}" class="form-control"></div>
        <button type="submit" class="btn btn-warning">Actualizar</button>
    </form>
</div>
{% endblock %}
```

#### 3.5 Rutina Personalizada (Pasos 56, 57)
Carpeta: `members/templates/rutina_personalizada/`

**agregar_rutina_personalizada.html**
```html
{% extends 'base.html' %}
{% block content %}
<div class="card p-4">
    <h3>Crear Rutina Personalizada</h3>
    <form method="POST">
        {% csrf_token %}
        <div class="mb-3"><label>Socio:</label>
            <select name="socio" class="form-select">
                {% for s in socios %}
                <option value="{{ s.id }}">{{ s.nombre }} {{ s.apellido }}</option>
                {% endfor %}
            </select>
        </div>
        <div class="mb-3"><label>Entrenador Asignado:</label>
            <select name="entrenador" class="form-select">
                {% for e in entrenadores %}
                <option value="{{ e.id }}">{{ e.nombre }} {{ e.apellido }}</option>
                {% endfor %}
            </select>
        </div>
        <div class="mb-3"><label>Objetivo:</label><input type="text" name="objetivo" class="form-control"></div>
        <div class="mb-3"><label>Descripción Ejercicios:</label><textarea name="descripcion_ejercicios" class="form-control" rows="4"></textarea></div>
        <div class="mb-3"><label>Frecuencia:</label><input type="text" name="frecuencia" class="form-control" placeholder="Ej: 3 veces por semana"></div>
        <div class="mb-3"><label>Duración (Semanas):</label><input type="number" name="duracion_semanas" class="form-control"></div>
        <button type="submit" class="btn btn-success">Guardar</button>
    </form>
</div>
{% endblock %}
```

**ver_rutinas_personalizadas.html**
```html
{% extends 'base.html' %}
{% block content %}
<h3>Rutinas Personalizadas</h3>
<a href="{% url 'agregar_rutina_personalizada' %}" class="btn btn-primary mb-3">Agregar</a>
<table class="table table-striped">
    <thead class="table-dark">
        <tr><th>Socio</th><th>Objetivo</th><th>Entrenador</th><th>Acciones</th></tr>
    </thead>
    <tbody>
        {% for r in rutinas %}
        <tr>
            <td>{{ r.socio }}</td>
            <td>{{ r.objetivo }}</td>
            <td>{{ r.entrenador }}</td>
            <td>
                <a href="{% url 'actualizar_rutina_personalizada' r.id %}" class="btn btn-info btn-sm">Editar</a>
                <a href="{% url 'borrar_rutina_personalizada' r.id %}" class="btn btn-danger btn-sm" onclick="return confirm('¿Eliminar?');">Borrar</a>
            </td>
        </tr>
        {% endfor %}
    </tbody>
</table>
{% endblock %}
```

**actualizar_rutina_personalizada.html**
```html
{% extends 'base.html' %}
{% block content %}
<div class="card p-4">
    <h3>Actualizar Rutina</h3>
    <form action="{% url 'realizar_actualizacion_rutina_personalizada' rutina.id %}" method="POST">
        {% csrf_token %}
        <div class="mb-3"><label>Socio:</label>
            <select name="socio" class="form-select">
                {% for s in socios %}
                <option value="{{ s.id }}" {% if rutina.socio.id == s.id %}selected{% endif %}>{{ s.nombre }} {{ s.apellido }}</option>
                {% endfor %}
            </select>
        </div>
        <div class="mb-3"><label>Entrenador:</label>
            <select name="entrenador" class="form-select">
                {% for e in entrenadores %}
                <option value="{{ e.id }}" {% if rutina.entrenador.id == e.id %}selected{% endif %}>{{ e.nombre }} {{ e.apellido }}</option>
                {% endfor %}
            </select>
        </div>
        <div class="mb-3"><label>Objetivo:</label><input type="text" name="objetivo" value="{{ rutina.objetivo }}" class="form-control"></div>
        <div class="mb-3"><label>Ejercicios:</label><textarea name="descripcion_ejercicios" class="form-control" rows="4">{{ rutina.descripcion_ejercicios }}</textarea></div>
        <div class="mb-3"><label>Frecuencia:</label><input type="text" name="frecuencia" value="{{ rutina.frecuencia }}" class="form-control"></div>
        <div class="mb-3"><label>Duración (Semanas):</label><input type="number" name="duracion_semanas" value="{{ rutina.duracion_semanas }}" class="form-control"></div>
        <button type="submit" class="btn btn-warning">Actualizar</button>
    </form>
</div>
{% endblock %}
```

Con esto, tu proyecto cumple con el requisito de tener todos los módulos funcionales, con su estructura de archivos, vistas sin formularios de Django, y diseño Bootstrap. ¡Asegúrate de que el servidor esté corriendo (`python manage.py runserver 8059`) y verifica cada sección desde el menú de navegación!

### Parte 7: Ejecución Final

**67. Ejecutar servidor:**
Asegúrate de que no haya errores en la terminal donde corre Django. Si se detuvo, ejecuta nuevamente:
```bash
python manage.py runserver 8059
```
Ve a tu navegador: `http://127.0.0.1:8059`.
