
# Corpus documental y archivo de evidencias — TFM sobre gobernanza de datos y privacidad en servicios de IA generativa


Este repositorio acompaña al Trabajo de Fin de Máster **Extracción y gobernanza de datos en plataformas de IA generativa: opacidad, asimetría y privacidad en Claude y ChatGPT
**, (Máster en Medios Comunicación y Cultura, Facultat de Ciències de la Comunicació, Universitat Autònoma de Barcelona, 2026).

Contiene los materiales que dan soporte empírico y verificable al trabajo:

1. El **corpus documental**: las fuentes públicas de Anthropic y OpenAI analizadas (precios, términos de servicio, políticas de privacidad, preguntas frecuentes y entradas de blog), capturadas mediante un protocolo de *snapshot* y archivadas en tres formatos.
2. Las **huellas de integridad (SHA-256)** de cada archivo, que permiten comprobar que ningún documento se ha alterado desde su captura.
3. Los **archivos de evidencia** con la codificación `[E]`/`[G]` empleada en las tablas del anexo del TFM.

El objetivo es garantizar la **verificabilidad** y el **valor de archivo** del estudio: dado que las páginas analizadas son dinámicas y cambian sin previo aviso, este repositorio «congela» la versión efectivamente consultada y documenta cómo se obtuvo.


---

## Estructura del repositorio

```
.
├── README.md                              ← este archivo
├── LICENSE                                ← licencia de la documentación propia (ver "Derechos y licencia")
├── SHA256SUMS.txt                         ← (generado) huellas en formato estándar, verificable con sha256sum
├── generar_manifiesto_hashes.py           ← utilidad para calcular y rellenar los hashes
├── evidencias/
│   └── evidencias_citadas_en_tablas.md   ← solo las citadas en las tablas del TFM ([E]/[G])
└── fuentes/
    ├── anthropic/
    │   ├── consumer_terms/
    │   │   ├── consumer_terms.html         ← copia capturada (original)
    │   │   ├── consumer_terms.md           ← versión en Markdown (derivada, para el análisis)
    │   │   └── consumer_terms.pdf          ← copia legible "congelada"
    │   ├── privacy_policy/
    │   ├── pc_con_10023548/
    │   ├── pc_con_10023580/
    │   ├── pricing/
    │   └── blog_consumer_update/
    └── openai/
        ├── privacy_policy_eu/
        ├── terms_of_use_eu/
        ├── privacy_policy_us/
        ├── help_5722486/
        ├── pricing/
        └── transparency_moderation/
```


---

## Corpus: documentos incluidos

Todas las fechas de captura corresponden al protocolo de *snapshot* descrito más abajo. La «última modificación declarada» es la que figuraba en la propia página (cuando la había).

### Anthropic

| Documento | URL | Captura | Últ. modificación |
|---|---|---|---|
| Consumer terms of service | https://www.anthropic.com/legal/consumer-terms | 2026-04-30 | 2025-10-08 |
| Privacy policy | https://www.anthropic.com/legal/privacy | 2026-04-30 | 2025-10 |
| How long do you store my data? (Centro de privacidad) | https://privacy.claude.com/en/articles/10023548-how-long-do-you-store-my-data | 2026-04-30 | s.f. |
| Is my data used for model training? (Centro de privacidad) | https://privacy.claude.com/en/articles/10023580-is-my-data-used-for-model-training | 2026-04-30 | s.f. |
| Pricing (Claude) | https://claude.com/pricing | 2026-04-30 | s.f. |
| Updates to our consumer terms and privacy policy (blog) | https://www.anthropic.com/news/updates-to-our-consumer-terms | 2026-04-30 | 2025-08-28 |

### OpenAI

| Documento | URL | Captura | Últ. modificación |
|---|---|---|---|
| EU privacy policy | https://openai.com/policies/eu-privacy-policy/ | 2026-04-30 | 2026-04-01 |
| EU terms of use | https://openai.com/policies/eu-terms-of-use/ | 2026-04-30 | 2026-01-16 |
| US privacy policy | https://openai.com/policies/us-privacy-policy/ | 2026-04-30 | 2026-02-09 |
| How your data is used to improve model performance (Centro de ayuda) | https://help.openai.com/en/articles/5722486-how-your-data-is-used-to-improve-model-performance | 2026-04-30 | s.f. |
| Pricing (ChatGPT) | https://chatgpt.com/pricing/ | 2026-04-30 | s.f. |
| Transparency and content moderation | https://openai.com/transparency-and-content-moderation/ | 2026-05-23 | 2026-05-04 |

El detalle completo, incluido el hash de cada archivo, está en **`manifiesto.csv`**.

---

## Protocolo de captura (*snapshot*)

Para cada fuente se registró:

- la **URL completa**, que permite la verificación posterior;
- la **fecha de captura**, que sitúa temporalmente el contenido frente a elementos dinámicos;
- una **copia archivada** del contenido en **tres formatos** (HTML, Markdown y PDF);
- una **huella de integridad SHA-256**, que permite demostrar que el archivo no se ha alterado desde la captura.

La descarga y la conversión a los tres formatos se automatizaron con **Claude Code**. Sobre cada archivo descargado se verificó **manualmente** que el contenido capturado se correspondía con la fuente original antes de incorporarlo al corpus. El procedimiento combina, por tanto, la captura automatizada con la validación humana del material analizado.

---

## Formatos y a qué corresponde el hash

| Formato | Rol |
|---|---|
| **HTML** | Copia del documento **tal como se capturó** (artefacto primario; es el más cercano a la fuente original). |
| **Markdown** | Versión **derivada y limpia** del HTML, empleada para la lectura y el análisis del contenido. |
| **PDF** | Copia **legible y de presentación fija**, pensada para consulta y archivo. |

Se proporciona el hash SHA-256 de **todos** los archivos (los tres formatos de cada documento), de modo que cualquiera de ellos puede verificarse de forma independiente. La huella de referencia del documento original es la del **HTML**.

---

## Verificación de integridad (SHA-256)

Para comprobar que los archivos no se han alterado:

**Linux:**
```bash
sha256sum -c SHA256SUMS.txt
```

**macOS:**
```bash
shasum -a 256 -c SHA256SUMS.txt
```

**Windows (PowerShell):**
```powershell
Get-FileHash .\fuentes\anthropic\consumer_terms\consumer_terms.html -Algorithm SHA256
```


### Generar / rellenar los hashes

Coloca los archivos del corpus en sus carpetas dentro de `fuentes/` y ejecuta, desde la raíz del repositorio:

```bash
python generar_manifiesto_hashes.py
```

El script recorre `manifiesto.csv`, calcula el SHA-256 de cada archivo existente, rellena la columna `sha256` y escribe además `SHA256SUMS.txt` en formato estándar. Si algún archivo aún no está, deja `PENDIENTE` y avisa.

---

## Archivos de evidencia

En `evidencias/` se incluyen **dos** ficheros, con funciones distintas:

- **`evidencias_citadas_en_tablas.csv`** — contiene únicamente las evidencias efectivamente citadas en las tablas del TFM. Es el complemento directo del documento: permite rastrear cada código `[Exxx]`/`[Gxxx]` hasta su cita literal, empresa y documento fuente.


### Convenciones de codificación

| Código | Significado |
|---|---|
| `[Exxx]` | Cita textual con fuente documentada en el archivo de evidencias. |
| `[Gxxx]` | Ausencia: la fuente consultada **no** contiene esa información. |

> **Antes de publicar**, conviene comprobar que todos los códigos `[E]`/`[G]` que aparecen en el TFM existen y coinciden exactamente en `evidencias_citadas_en_tablas.csv` (numeración, empresa y documento fuente). El registro de citas se realizó manualmente y los identificadores secuenciales se asignaron con Claude Code.

---

## Nota temporal y limitaciones

El corpus refleja el estado de cada documento **en su fecha de captura**. Anthropic y OpenAI modifican sus términos de servicio y políticas de privacidad con relativa frecuencia, por lo que el contenido archivado puede no coincidir con la versión vigente en el momento de la consulta. Esa es, precisamente, la razón de ser de este repositorio: ofrecer una referencia estable y verificable del régimen documental analizado en el TFM.

---

## Derechos y licencia

- **Documentos capturados de terceros** (carpeta `fuentes/`): los términos de servicio, políticas de privacidad, páginas de precios, preguntas frecuentes y entradas de blog son propiedad de **Anthropic** y **OpenAI**, respectivamente, y conservan su copyright original. Se reproducen aquí, sin ánimo de lucro y de forma íntegra, **con fines exclusivos de investigación académica, verificación y archivo**, como soporte documental del TFM. Todos los derechos pertenecen a sus titulares.


- [ ] Título del TFM
- [ ] Nombre y correo de la autora
- [ ] Nombre del máster
- [ ] Nombre definitivo del repositorio
- [ ] DOI / URL (si usas Zenodo u OSF)
- [ ] Colocar los archivos del corpus en `fuentes/` y ejecutar `generar_manifiesto_hashes.py`
- [ ] Añadir el archivo `LICENSE` (CC BY 4.0)
- [ ] Sustituir `[URL del repositorio]` en el TFM por la URL/DOI real
