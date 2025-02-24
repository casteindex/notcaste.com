+++
title = 'C/C++ formato automático en Visual Studio'
date = 2025-02-23T22:14:54-06:00
tags = ['programming', 'cpp']
url = 'formato-automatico-visual-studio'
draft = false
+++

ClangFormat es una herramienta para formatear código de C/C++ automáticamente. Nos ayuda a mantener un estilo consistente en nuestros archivos y a no tener que procuparnos por el orden, indentar correctamente, espacios, etc.

## ¿Cómo activarlo en Visual Studio?

1. **Abrir Visual Studio**.

2. **Ir al menú de Opciones**:

    - Hacer clic en **Herramientas** en la barra de menú en la parte superior de la ventana.
    - En el menú desplegable, seleccionar **Opciones...**.

3. **Navegar a las opciones de formato de C++**:

    - En la ventana de **Opciones**, en el panel izquierdo, expandir el apartado **Editor de texto**.
    - Luego, seleccionar **C++**.
    - Finalmente, seleccionar **Formato**.

4. **Habilitar ClangFormat**:
    - Asegurarse de que la opción de **Habilita la compatibilidad con ClangFormat** esté activada.
    - Definir un **Estilo de formato predeterminado**. Yo recomiendo el de Google porque es muy opinionado.

## Funcionamiento Automático

Con la configuración descrita anteriormente, se puede formatear cualquier archivo de código fuente con `Ctrl+K, Ctrl+F` (para formatear la selección) o `Ctrl+K, Ctrl+D` (para formatear el documento entero).

Sin embargo, si se prefiere aplicar el formato automáticamente al guardar el archivo, se puede hacer siguiendo estos pasos:

1. **Ir a la tienda de Extensiones**:

    - Hacer clic en **Extensiones** en la barra de menú en la parte superior de la ventana.
    - En el menú desplegable, seleccionar **Administrar extensiones...**.

2. **Instalar "Format document on Save"**.
    - Buscar la extensión e instalarla.
    - Reiniciar Visual Studio.

## Configuración adicional

Visual Studio busca el archivo `.clang-format` en la ruta del directorio de inicio. Si no encuentra alguno, usa el predeterminado (Google, en nuestro caso).

Personalmente, prefiero usar uno personalizado. Las opciones disponibles para definir el estilo del formato se pueden encontrar [aquí](https://clang.llvm.org/docs/ClangFormatStyleOptions.html).

A continuación, dejo mi configuración basada en el estilo de Google. Para crear el archivo directamente en el directorio de usuario, solo es necesario ejecutar el siguiente comando en PowerShell:

```powershell
Set-Content -Path "$HOME\.clang-format" -Value @"
BasedOnStyle: Google
IndentWidth: 4
AlignAfterOpenBracket: DontAlign
AllowShortFunctionsOnASingleLine: Empty
AllowShortLoopsOnASingleLine: false
"@
```

Este comando generará el archivo de configuración automáticamente con las opciones deseadas.
