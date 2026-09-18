# Portafolio — jorgedanielgallo.github.io

Sitio personal de Jorge Gallo. Una sola página estática, sin framework, sin
build. Se despliega copiando estos archivos a la raíz del repositorio
`jorgedanielgallo/jorgedanielgallo.github.io`.

```
index.html      La página completa (HTML + CSS + un script de 20 líneas para el tema)
404.html        Página de error, misma identidad visual
robots.txt      Permite indexación completa
cv/             Aquí va tu PDF (ver paso 1)
```

---

## Qué cambió frente al sitio anterior

**Lo que salió, y por qué:**

| Quitado | Razón |
|---|---|
| Fecha de nacimiento (22-dic-1996) y edad | Es un pasivo real en postulaciones a EE.UU.: discriminación por edad. Ningún sitio de ingeniero senior la publica |
| WhatsApp e Instagram | Un reclutador no te escribe por Instagram; sí lo usa para formarse una opinión |
| Teléfono visible | Se retiró del sitio (sigue en el CV, que llega solo a quien postulas). Evita scraping y spam |
| Barras de "proficiency" (Java 100%, Python 100%) | Un 100% no sobrevive una entrevista senior. Nadie es 100% en nada, y declararlo resta credibilidad en vez de sumarla |
| "15+ projects leading and designing" | Cifra no verificable. Se reemplazó por cinco proyectos que se pueden abrir y leer |

**Lo que entró:**

- **Sección "Selected work"** con los cinco repositorios, cada uno con el
  problema que resuelve y tres o cuatro decisiones técnicas concretas. Es la
  sección más larga del sitio a propósito: es lo que un tech lead lee.
- **Experiencia con la línea de tiempo corregida** (Rootstack jun–sep 2026, no
  2023–2026) y los nombres legales completos de las empresas.
- **Toolkit sin porcentajes**: solo qué usas, agrupado por rol.
- **Nota de zona horaria** (UTC−05:00) en el hero y en contacto. Para vacantes
  remotas en EE.UU. el solapamiento horario es criterio de filtro real.
- Tema claro y oscuro con interruptor, accesible por teclado, responsive hasta
  390 px, meta tags de Open Graph para cuando compartas el enlace.

El diseño es una hoja de contabilidad: líneas finas en vez de tarjetas, números
tabulares, tipografía mono para etiquetas y datos, Spectral para titulares. Es
coherente con lo que construyes y no se parece a una plantilla.

---

## Cómo publicarlo

### Paso 1 — tu CV en PDF

El botón "Résumé (PDF)" del hero apunta a `cv/Jorge-Gallo-CV.pdf`. Antes de
publicar, haz una de las dos cosas:

```powershell
# Opción A: pones el PDF donde el botón lo espera
New-Item -ItemType Directory -Force -Path .\cv
Copy-Item "C:\ruta\a\tu\JORGE_GALLO_CV.pdf" .\cv\Jorge-Gallo-CV.pdf
```

**Opción B:** si prefieres no publicar el CV, borra esa línea de `index.html`
(está marcada con un comentario `<!-- Drop your PDF ... -->`).

Un botón que lleva a un 404 hace más daño que no tener botón.

### Paso 2 — subirlo

```powershell
git clone https://github.com/jorgedanielgallo/jorgedanielgallo.github.io.git
Set-Location jorgedanielgallo.github.io

# Guarda el sitio viejo por si quieres volver
git checkout -b sitio-anterior
git push -u origin sitio-anterior
git checkout main

# Borra el contenido viejo y copia el nuevo
Get-ChildItem -Exclude .git | Remove-Item -Recurse -Force
Copy-Item -Path "C:\ruta\a\esta\carpeta\*" -Destination . -Recurse

git add -A
git commit -m "feat: rebuild the site around the five projects"
git push
```

GitHub Pages publica en uno o dos minutos. Revisa
<https://jorgedanielgallo.github.io/> en el teléfono además del computador.

### Paso 3 — después de publicar

1. Verifica que los cinco enlaces a los repositorios funcionen (solo funcionan
   una vez que hayas corrido `publish-to-github.ps1`; mientras tanto dan 404).
2. Pasa el enlace por <https://pagespeed.web.dev/> — debería salir casi
   perfecto, es un archivo estático sin JavaScript de terceros.
3. Actualiza el enlace del sitio en tu perfil de LinkedIn y en el CV.

---

## Editarlo después

Todo está en `index.html`, en este orden: tokens de color → estilos → contenido
→ script del tema. Para cambiar la paleta, toca solo el bloque `:root` (y su
gemelo en `[data-theme="dark"]`). Para agregar un proyecto, copia un bloque
`<li class="entry">` completo. No hay build: guardas, abres el archivo en el
navegador, y eso es exactamente lo que verá la gente.
