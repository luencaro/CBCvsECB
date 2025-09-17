# Análisis de Maleabilidad en AES-CBC vs AES-ECB

Este repositorio contiene un laboratorio práctico para explorar la maleabilidad en los modos de cifrado AES-CBC y AES-ECB, demostrando las diferencias de seguridad entre ambos modos.

## 📋 Descripción

El proyecto implementa un cifrador de archivos usando AES en modos CBC y ECB, permitiendo experimentar con diferentes tipos de ataques de maleabilidad para comprender conceptos fundamentales de criptografía:

- **Confidencialidad vs Integridad**
- **Maleabilidad en modos de cifrado**
- **Vulnerabilidades específicas de ECB y CBC**

## 🔧 Funcionalidades

### Cifrado y Descifrado
- Implementación de AES en modo CBC (Cipher Block Chaining)
- Implementación de AES en modo ECB (Electronic Codebook)
- Soporte para archivos de cualquier tamaño

### Herramientas de Análisis
- **Bit Flipper**: Modifica bits específicos en el texto cifrado
- **Block Swapper**: Intercambia bloques completos del ciphertext
- **Comparadores de archivos**: Análisis byte por byte y por bloques

## 🚀 Uso

### Requisitos
```python
from Crypto.Cipher import AES
from Crypto import Random
from Crypto.Hash import SHA256
from Crypto.Util.Padding import pad
```

### Ejemplos de uso

```python
# Cifrar un archivo
encrypt("CBC", getKey("contraseña"), "archivo.pdf")

# Aplicar bit flipping
bit_flipper("archivo.pdf.enc", "archivo_modificado.pdf.enc")

# Intercambiar bloques
swap_blocks("archivo.pdf.enc", "archivo_swap.pdf.enc", 16, 3, 5)

# Descifrar y comparar
decrypt("CBC", getKey("contraseña"), "archivo_modificado.pdf.enc")
compare_files_per_block("archivo_original.pdf", "archivo_descifrado.pdf")
```

## 🧪 Experimentos Implementados

### 1. Bit Flipping Attack (CBC)
- Modifica un bit en el bloque Ck
- **Resultado**: Corrompe Pk-1 completamente y causa bit flip en Pk

### 2. Block Swapping (CBC)
- Intercambia bloques Ci y Cj
- **Resultado**: Corrompe exactamente 4 bloques (Pi-1, Pi, Pj-1, Pj)

### 3. Comparación con ECB
- **Bit flipping**: Solo afecta un bloque
- **Block swapping**: Intercambio limpio de bloques

## 📊 Resultados Esperados

| Ataque | CBC | ECB |
|--------|-----|-----|
| Bit Flip | 2 bloques corrompidos | 1 bloque corrompido |
| Block Swap | 4 bloques corrompidos | Intercambio limpio |

## 🔒 Lecciones de Seguridad

- **ECB es inseguro** para datos estructurados (revela patrones)
- **CBC sin autenticación** es vulnerable a ataques de maleabilidad
- **Confidencialidad ≠ Integridad**
- La necesidad de usar modos autenticados (AEAD) como GCM

## 📁 Estructura del Proyecto

```
├── AES-CBC.ipynb              # Notebook principal con implementaciones
├── Criptografia_Actividad_I.pdf  # Documento con instrucciones del laboratorio
├── test.pdf                   # Archivo de prueba
└── Resultados/               # Resultados de experimentos
    ├── CBC - Bit flip/
    ├── CBC - Block Swap/
    ├── ECB - Bit flip/
    └── ECB - Block Swap/
```

