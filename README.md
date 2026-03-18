# CREACION DE LA APLICACIÓN.PY
Este proyecto es una aplicación gráfica desarrollada con Flet que simula una tienda de tecnología con carrito y favoritos.

**1. Importaciones**
```python
import flet as ft
from product_card import ProductCard
```

- flet: Framework para crear interfaces gráficas en Python. <br>
- ProductCard: Componente personalizado que representa cada producto (tarjeta visual).

**2. Lista de productos**
```python
productos = [
    {"id": 1, "nombre": "Laptop Gamer", ...},
    ...
]
```

- Es una lista de diccionarios.<br>
- Cada producto contiene:<br>
  - id: identificador único<br>
  - nombre: nombre del producto<br>
  - descripcion: características<br>
  - precio: costo<br>
  - ruta_imagen: imagen del producto (en carpeta assets)<br>

 **3. Función principal (main)**
 ```python
def main(page: ft.Page):
```
- Punto de entrada de la aplicación.
- page representa la ventana principal.

Configuración inicial:
```python
page.title = "TECHNOLOGY STORE"
page.scroll = "auto"
page.bgcolor = "#000000"
page.padding = 20
page.assets_dir = "assets"
```

- Define:<br>
  - Título de la app<br>
  - Scroll automático<br>
  - Fondo negro<br>
  - Espaciado interno<br>
  - Carpeta de imágenes<br>

```python
carrito = []
favoritos = []
```
**4. Estado de la aplicación**
- Listas que almacenan:<br>
  - Productos en carrito<br>
  - Productos favoritos<br>

Contadores visuales:
```python
carrito_text = ft.Text("0", size=14)
favoritos_text = ft.Text("0", size=14)
```
- Muestran la cantidad actual en la interfaz

**5. Funciones auxiliares**

📢 Mostrar mensaje
```python
def mostrar_mensaje(msg):
```
- Muestra un SnackBar (mensaje emergente)

🛒Agregar al carrito
```python
def agregar_carrito(producto):
```
- Agrega producto a carrito
- Actualiza contador
- Muestra mensaje

❤️ Agregar/quitar favorito
```python
def agregar_favorito(producto):
```
- Si no está → lo agrega
- Si ya está → lo elimina
- Actualiza contador

**6. Header (encabezado)**
```python
header = ft.Row([...])
```
# TECHNOLOGY STORE

---

## 📋 Panel de Usuario

| ❤️ Favoritos | 🛒 Carrito |
| :---: | :---: |
| [Ver lista] | [Finalizar compra] |

---

**7. Creación de tarjetas de productos**
```python
tarjetas = []
for p in productos:
```
Se recorre cada producto y se crea una tarjeta:
```python
card = ProductCard(...)
```
🛒 Evento: agregar al carrito
```python
card.agregar = lambda e, prod=p: agregar_carrito(prod)
```
- Asigna una función al botón de la tarjeta.
- Usa lambda para capturar el producto actual (prod=p).

❤️ Evento: favoritos (con handler dinámico)
```python
def make_fav_handler(prod, card_ref):
```
- Crea una función personalizada por tarjeta.

Dentro:
```python
if prod in favoritos:
    card_ref.fav_icon.value = "❤️"
else:
    card_ref.fav_icon.value = "🤍"
```
Cambia el ícono visual según estado.


📦 Contenedor de tarjeta
```python
ft.Container(
    content=card,
    padding=5
)
```
- Añade margen visual a cada tarjeta.

**8. Grid de productos**
```python
grid = ft.Row(
    controls=tarjetas,
    wrap=True,
    spacing=15,
    run_spacing=15
)
```
- Muestra productos en forma de rejilla adaptable.
- wrap=True: salta a la siguiente línea automáticamente.

**9. Renderizado en pantalla**
```python
page.add(
    header,
    ft.Container(height=10),
    grid
)
```
- Agrega:
  1. Encabezado
  2. Espacio
  3. Productos

**10. Ejecución de la app**
```python
if __name__ == "__main__":
    ft.app(target=main, assets_dir="assets")
```
- Inicia la aplicación.
- Usa main como función principal.

# CREACIÓN DE LA PAGINA WEB APARTIR DE LA APP
Despliegue en Netlify
¿Qué es Netlify?
Netlify es una plataforma gratuita que permite publicar aplicaciones web en internet con solo arrastrar una carpeta.

¿Cómo se preparó la app para web?
Flet permite convertir una aplicación de escritorio en web usando el comando flet publish. Este comando genera una carpeta dist/ con todos los archivos necesarios para el despliegue.

Se ejecutó el siguiente comando en la terminal dentro de la carpeta del proyecto:

flet publish main.py
Esto generó automáticamente:

- dist/index.html — página principal
- dist/manifest.json — configuración de la app
- dist/version.json — versión de Flet
- dist/app.tar.gz — código comprimido de la app

Pasos para desplegar en Netlify:
1. Entrar a netlify.com e iniciar sesión
2. En el panel principal ir a:
- Sites → Add new project → Deploy manually
3. Arrastrar la carpeta dist/ generada por flet publish a la zona de deploy de Netlify
4. Netlify procesa los archivos automáticamente y genera un link único:
- [https://nombre-aleatorio.netlify.app](https://resonant-selkie-196ccb.netlify.app/)
5. Se puede personalizar el nombre del sitio desde:
- Site configuration → Site details → Change site name
Resultado:
La app quedó disponible públicamente en internet sin necesidad de un servidor propio.
