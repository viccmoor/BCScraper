# BCScraper

**BCScraper** es un scraper ligero y fácil de usar que permite obtener información de cursos desde [buscacursos.uc.cl](https://buscacursos.uc.cl) sin necesidad de proxies.  
Ideal para estudiantes, desarrolladores o cualquier persona que necesite automatizar la extracción de datos de los cursos UC.

---

## Características

- Obtiene información completa de los cursos: NRC, sigla, nombre, profesor(es), campus, créditos, vacantes y horarios.
- Permite buscar cursos por:
  - Sigla
  - Nombre
  - Profesor
  - NRC específico
- Obtiene automáticamente los períodos disponibles.
- No requiere proxies ni autenticación.

---

## Instalación

> [!IMPORTANT]
> **Se requiere Python 3 o superior**

```bash
# Linux/macOS
python3 -m pip install -U bcscraper

# Windows
py -3 -m pip install -U bcscraper
```

## Ejemplo rápido

```python
from bcscraper import (
    buscar_sigla,
    buscar_profesor,
    buscar_curso,
    obtener_curso,
    obtener_periodos
)

# Obtener los períodos disponibles
periodos = obtener_periodos()
print("Períodos disponibles:", periodos)

# Tomamos el primer período como ejemplo
periodo = periodos[0]

# Buscar cursos por sigla
cursos_sigla = buscar_sigla(periodo, "MAT1610")
print("\nCursos por sigla MAT1610:")
for c in cursos_sigla:
    print(f"{c.nrc} - {c.sigla} Sección {c.seccion} - {c.nombre}")

# Buscar cursos por profesor
cursos_profesor = buscar_profesor(periodo, "Nombre Apellido")
print("\nCursos del profesor Nombre Apellido:")
for c in cursos_profesor:
    print(f"{c.sigla} - {c.nombre} - Profesores: {', '.join(c.profesor)}")

# Buscar cursos por nombre
cursos_nombre = buscar_curso(periodo, "Cálculo I")
print("\nCursos con nombre 'Cálculo I':")
for c in cursos_nombre:
    print(f"{c.sigla}-{c.seccion} - {c.nombre} - NRC: {c.nrc}")

# Obtener un curso específico por NRC
curso_nrc = obtener_curso(periodo, "14778")
if curso_nrc:
    print("\nDetalles del curso con NRC 14778:")
    print(f"{curso_nrc.sigla}-{curso_nrc.seccion} {curso_nrc.nombre}")
    print(f"Profesor(es): {', '.join(curso_nrc.profesor)}")
    print(f"Vacantes disponibles: {curso_nrc.vacantes_disponibles}")

    print("Horarios:")
    for h in curso_nrc.horario:
        print(f"  {h.dia} Módulo {h.modulo} - {h.tipo} en {h.sala}")
```