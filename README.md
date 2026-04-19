Video Text Remover Pro
Elimina texto o marcas de agua de videos usando tu GPU NVIDIA.
Historia del Proyecto
Este proyecto comenzó con una petición simple: crear una herramienta en Python para eliminar texto de una zona específica de un video, seleccionada manualmente por el usuario.
Version 1.0 - OpenCV Basico
La primera version usaba OpenCV con cv2.inpaint() para rellenar la zona seleccionada y cv2.selectROI() para la seleccion interactiva.
Problema: Era muy lento. Procesar 1 hora de video podia tomar entre 1.5 y 3 horas porque todo se ejecutaba en la CPU, frame por frame.
Version 2.0 - Multiprocessing
Se intento acelerar el procesamiento usando ProcessPoolExecutor para procesar bloques de frames en paralelo.
Resultado: La mejora fue minima. El overhead de serializar los arrays de NumPy entre procesos anulaba la ganancia de velocidad.
Version 3.0 - FFmpeg + NVENC (Cambio Clave)
Se reemplazo OpenCV por FFmpeg con el filtro delogo para eliminar el texto y el codec h264_nvenc para codificar el video usando la GPU NVIDIA.
Resultado: La velocidad mejoro drasticamente. 1 hora de video ahora se procesa en 5-6 minutos (10-12x mas rapido).
Version 4.0 - Version Actual (Profesional)
Se agregaron mejoras de experiencia de usuario y estabilidad:
Selector de zona estable en Windows (soluciona el bug de pantalla blanca)
Modo de prueba de 30 segundos antes de procesar todo el video
Tres niveles de calidad: Rapido, Balanceado, Calidad
Barra de progreso con tiempo estimado restante
Validacion automatica de FFmpeg y soporte NVENC
Conservacion automatica del audio original
Caracteristicas
Seleccion visual de la zona con el mouse
Aceleracion por GPU NVIDIA (NVENC)
Soporte para videos a 60 fps
El audio original se conserva intacto
Modo de prueba para validar resultados antes de procesar todo
Progreso en tiempo real con velocidad y ETA
Validaciones de entrada y manejo de errores
Requisitos
Hardware
GPU NVIDIA con soporte NVENC (GTX 10-series o superior)
8 GB de RAM minimo (16 GB recomendado)
Espacio en disco: al menos 2x el tamaño del video a procesar
Software
Python 3.10 o superior
FFmpeg con soporte NVENC (descargar desde gyan.dev)
Paquetes de Python: opencv-python, numpy
