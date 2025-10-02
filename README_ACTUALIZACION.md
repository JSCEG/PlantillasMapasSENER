# 🔄 Actualización de Índices - SENER

Este conjunto de herramientas te permite actualizar el archivo `brillantes.js` con los nuevos índices del archivo Excel y realizar análisis por cuartiles.

## 📋 Nuevos Campos Agregados

Los siguientes campos se han agregado al análisis:

| Campo Excel | Campo JavaScript | Descripción |
|-------------|------------------|-------------|
| `indice_geotermia` | `indice_geo` | Índice de Geotermia |
| `Índice General de Precariedad (old)` | `indice_general_precariedad_old` | Índice anterior de precariedad |
| `Índice Prioritario Por Estado` | `indice_prioritario_estado` | Priorización por entidad |
| `indice_general_precariedad_clipped` | `indice_general_precariedad_clipped` | Nuevo índice de precariedad |
| `Código Geoespacial INEGI` | `CVEGEO` | Clave geográfica INEGI |
| `Indice_Deuda_CFE` | `indice_deuda_cfe` | Índice de deuda con CFE |

## 🛠️ Herramientas Disponibles

### 1. Convertidor Web (Recomendado)
**Archivo:** `convertir_excel_a_json.html`

- Interfaz web fácil de usar
- Drag & drop para archivos Excel
- Vista previa de datos
- Actualización automática de brillantes.js
- Exportación en múltiples formatos

**Uso:**
1. Abre `convertir_excel_a_json.html` en tu navegador
2. Arrastra o selecciona tu archivo Excel
3. Revisa la vista previa
4. Haz clic en "Actualizar brillantes.js"
5. Descarga el archivo actualizado

### 2. Script CLI (Para usuarios avanzados)
**Archivo:** `actualizar_brillantes_cli.js`

**Instalación:**
```bash
# Instalar dependencias
npm install xlsx

# O usar el package.json incluido
cp package_actualizar.json package.json
npm install
```

**Uso:**
```bash
# Sintaxis básica
node actualizar_brillantes_cli.js <archivo_excel> [archivo_brillantes]

# Ejemplo
node actualizar_brillantes_cli.js indicadores/BASE_FINAL_INDICES_MUN.xlsx indicadores/brillantes.js

# Ver ayuda
node actualizar_brillantes_cli.js --help
```

### 3. Análisis por Cuartiles
**Archivos:** `analisis_cuartiles.js` + `test_analisis_cuartiles.html`

Herramienta para analizar los índices y calcular cuartiles:

- Análisis estadístico completo
- Cálculo de cuartiles (Q1-Q4)
- Clasificación de municipios
- Exportación de reportes
- Visualización interactiva

**Uso:**
1. Abre `test_analisis_cuartiles.html` en tu navegador
2. Carga el archivo `brillantes.js` actualizado
3. Selecciona el índice a analizar
4. Genera reportes y exporta resultados

## 📊 Estructura de Datos Esperada

### Archivo Excel
El archivo Excel debe contener las siguientes columnas:

```
codigo | NOM_ENT | NOM_MUN | Nivel | numero_viviendas | indice_ingreso | indice_electrico | indice_pobreza_energetica | indice_sociodemografico | indice_geotermia | indice_problemas_electricos | indice_actividades_productivas_normalizado | Índice General de Precariedad (old) | Índice Prioritario Por Estado | indice_general_precariedad_clipped | Código Geoespacial INEGI | Indice_Deuda_CFE
```

### Ejemplo de fila:
```
5_26 | Coahuila de Zaragoza | Progreso | MUN | 981 | 47.15041 | 1.414435 | 52.4699 | 27.77867 | 1.545254 | 0 | 0.304207 | 4.03E-05 | 0.003037 | 0.000001 | 05026 | 0
```

## 🔧 Proceso de Actualización

### Paso a Paso:

1. **Preparar el Excel**
   - Asegúrate de que el archivo Excel tenga todas las columnas necesarias
   - Verifica que la columna "Código Geoespacial INEGI" esté presente
   - Los valores numéricos deben estar en formato correcto

2. **Hacer Backup**
   ```bash
   cp indicadores/brillantes.js indicadores/brillantes_backup.js
   ```

3. **Ejecutar la Actualización**
   - Usa la herramienta web o el script CLI
   - Revisa los logs para verificar que todos los municipios se actualizaron

4. **Verificar Resultados**
   - Abre `test_analisis_cuartiles.html`
   - Carga el archivo actualizado
   - Verifica que los nuevos campos estén presentes

5. **Reemplazar Archivo Original**
   ```bash
   cp indicadores/brillantes_actualizado.js indicadores/brillantes.js
   ```

## 📈 Análisis por Cuartiles

### Interpretación de Cuartiles:

- **Q1 (25%)**: Municipios con mejor situación (valores más bajos = menor impacto)
- **Q2 (50%)**: Municipios en situación buena
- **Q3 (75%)**: Municipios en situación regular
- **Q4 (100%)**: Municipios en situación crítica (valores más altos = mayor impacto)

### Índices Disponibles para Análisis:

1. **Índice de Ingreso** (`indice_ing`)
2. **Índice Eléctrico** (`indice_ele`)
3. **Índice de Pobreza Energética** (`indice_pob`)
4. **Índice Sociodemográfico** (`indice_soc`)
5. **Índice de Geotermia** (`indice_geo`) ⭐ NUEVO
6. **Índice de Problemas Eléctricos** (`indice_pro`)
7. **Índice de Actividades Productivas** (`indice_act`)
8. **Índice General de Precariedad (Anterior)** (`indice_general_precariedad_old`) ⭐ NUEVO
9. **Índice Prioritario Por Estado** (`indice_prioritario_estado`) ⭐ NUEVO
10. **Índice General de Precariedad (Nuevo)** (`indice_general_precariedad_clipped`) ⭐ NUEVO
11. **Índice de Deuda CFE** (`indice_deuda_cfe`) ⭐ NUEVO

## 🚨 Solución de Problemas

### Error: "No se encontraron datos del Excel para CVEGEO"
- Verifica que la columna "Código Geoespacial INEGI" esté presente
- Asegúrate de que los códigos tengan 5 dígitos (ej: 05026)

### Error: "El archivo brillantes.js no existe"
- Verifica la ruta del archivo
- Asegúrate de estar en el directorio correcto

### Error: "xlsx no está instalado"
```bash
npm install xlsx
```

### Los nuevos campos no aparecen
- Verifica que los nombres de las columnas en Excel coincidan exactamente
- Revisa los logs de la consola para errores de mapeo

## 📁 Archivos Generados

Después de la actualización tendrás:

- `brillantes_actualizado.js` - Archivo principal actualizado
- `indices_municipales.json` - Datos en formato JSON
- `analisis_cuartiles.json` - Resultados del análisis
- `reporte_completo.html` - Reporte visual

## 🔄 Integración con el Mapa

Una vez actualizado `brillantes.js`, los nuevos índices estarán disponibles automáticamente en:

- `mapa.js` - Para visualización en el mapa
- `impacto.js` - Para análisis de impacto
- `evaluacion_nacional.html` - Para evaluación nacional
- `evaluacion_entidad.html` - Para evaluación por entidad

## 📞 Soporte

Si encuentras problemas:

1. Revisa los logs de la consola del navegador
2. Verifica que todos los archivos estén en las rutas correctas
3. Asegúrate de que el Excel tenga el formato correcto
4. Haz backup antes de cualquier cambio importante

---

**Desarrollado para SENER - Subsecretaría de Planeación y Transición Energética**