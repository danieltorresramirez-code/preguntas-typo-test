
import streamlit as st

# 1. EL ARCHIVADOR (Nuestra base de datos de preguntas)
preguntas = [
    {
        "texto": "¿Cuál es el lenguaje de programación que estamos usando?",
        "opciones": ["Java", "Python", "C++", "JavaScript"],
        "correcta": "Python"
    },
    {
        "texto": "¿Qué comando se usa para ejecutar una app de Streamlit?",
        "opciones": ["python run", "streamlit run", "start streamlit"],
        "correcta": "streamlit run"
    },
    {
        "texto": "¿En qué año se lanzó la Web 1.0?",
        "opciones": ["1983", "1990", "2005"],
        "correcta": "1990"
    },
    {
        "texto": "¿Qué función de Streamlit se usa para mostrar un título grande?",
        "opciones": ["st.text()", "st.header()", "st.title()", "st.write()"],
        "correcta": "st.title()"
    },
    {
        "texto": "¿Cuál de estos es un componente de entrada de datos en Streamlit?",
        "opciones": ["st.button()", "st.image()", "st.balloons()", "st.code()"],
        "correcta": "st.button()"
    },
    {
        "texto": "¿Cómo se llama la herramienta de Python para instalar librerías?",
        "opciones": ["npm", "pip", "git", "apt-get"],
        "correcta": "pip"
    },
    {
        "texto": "¿Qué tipo de dato es 'Hola Mundo' en Python?",
        "opciones": ["Integer (int)", "Boolean (bool)", "String (str)", "Float"],
        "correcta": "String (str)"
    },
    {
        "texto": "¿Para qué sirve el comando 'st.sidebar'?",
        "opciones": ["Para crear una barra lateral", "Para cerrar la página", "Para cambiar el color de fondo"],
        "correcta": "Para crear una barra lateral"
    },
    {
        "texto": "En Python, ¿cuál es el símbolo para hacer un comentario de una línea?",
        "opciones": ["//", "/*", "#", "--"],
        "correcta": "#"
    }
]

# Configuración visual de la página
st.set_page_config(page_title="Examen de Programación", page_icon="💻")
st.title("🎓 Examen Interactivo Completo")
st.info("Responde las 9 preguntas para obtener tu calificación final.")

# 2. EL FORMULARIO
with st.form("quiz_form"):
    respuestas_usuario = []
   
    # Recorremos el archivador
    for i, pregunta in enumerate(preguntas):
        st.subheader(f"Pregunta {i+1}: {pregunta['texto']}")
        # Usamos una clave única para cada radio button basada en el índice
        eleccion = st.radio("Selecciona tu respuesta:", pregunta["opciones"], key=f"pregunta_{i}")
        respuestas_usuario.append(eleccion)
        st.write("---")

    boton_enviar = st.form_submit_button("Entregar Examen")

# 3. LA CORRECCIÓN
if boton_enviar:
    aciertos = 0
    total = len(preguntas)

    # Comparación de respuestas
    for i in range(total):
        if respuestas_usuario[i] == preguntas[i]["correcta"]:
            aciertos = aciertos + 1

    # Cálculo de la nota (ahora sobre 9 preguntas)
    nota = round((aciertos / total) * 10, 1)

    st.divider()
    st.header(f"Resultado final: {nota} / 10")
    st.write(f"Has acertado {aciertos} de {total} preguntas.")

    if nota >= 5:
        st.success("¡Excelente trabajo! Has superado el examen.")
        st.balloons()
    else:
        st.error("No has alcanzado el aprobado. ¡Repasa el código y vuelve a intentarlo!")
