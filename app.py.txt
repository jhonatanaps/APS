import streamlit as st

# Configuração da Página
st.set_page_config(page_title="APS - Análise de Milhares", layout="wide")

# Adicionando a Imagem de Fundo
page_bg_img = """
<style>
[data-testid="stAppViewContainer"] {
    background-image: url("7.jpg");
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
}
</style>
"""
st.markdown(page_bg_img, unsafe_allow_html=True)

# Título da Página
st.title("🔢 APS - Gerador de Milhares e Centenas 🎯")

# Inputs do Usuário
st.subheader("📝 Insira os dados para gerar suas milhares e centenas")

# Entrada para pedras de milhar
milhar1 = st.text_input("Digite a primeira pedra de milhar", max_chars=1)
milhar2 = st.text_input("Digite a segunda pedra de milhar", max_chars=1)

# Entrada para pedras de centena
centena1 = st.text_input("Digite a primeira pedra de centena", max_chars=1)
centena2 = st.text_input("Digite a segunda pedra de centena", max_chars=1)
centena3 = st.text_input("Digite a terceira pedra de centena", max_chars=1)
centena4 = st.text_input("Digite a quarta pedra de centena", max_chars=1)

# Entrada para bichos
bichos_escolhidos = st.text_area("Digite até 5 bichos (separados por vírgula)", placeholder="Exemplo: Cavalo, Galo, Leão")

# Dicionário dos bichos e dezenas
bichos_dict = {
    "Avestruz": [1, 2, 3, 4], "Águia": [5, 6, 7, 8], "Burro": [9, 10, 11, 12],
    "Borboleta": [13, 14, 15, 16], "Cachorro": [17, 18, 19, 20], "Cabra": [21, 22, 23, 24],
    "Carneiro": [25, 26, 27, 28], "Camelo": [29, 30, 31, 32], "Cobra": [33, 34, 35, 36],
    "Coelho": [37, 38, 39, 40], "Cavalo": [41, 42, 43, 44], "Elefante": [45, 46, 47, 48],
    "Galo": [49, 50, 51, 52], "Gato": [53, 54, 55, 56], "Jacaré": [57, 58, 59, 60],
    "Leão": [61, 62, 63, 64], "Macaco": [65, 66, 67, 68], "Porco": [69, 70, 71, 72],
    "Pavão": [73, 74, 75, 76], "Peru": [77, 78, 79, 80], "Touro": [81, 82, 83, 84],
    "Tigre": [85, 86, 87, 88], "Urso": [89, 90, 91, 92], "Veado": [93, 94, 95, 96],
    "Vaca": [97, 98, 99, 00]
}

# Função para gerar milhares e centenas
def gerar_milhares_centenas():
    if not milhar1 or not milhar2 or not centena1 or not centena2 or not centena3 or not centena4 or not bichos_escolhidos:
        st.warning("⚠️ Preencha todos os campos para gerar milhares e centenas!")
        return [], []

    pedras_milhar = [milhar1, milhar2]
    pedras_centena = [centena1, centena2, centena3, centena4]

    bichos = [b.strip().title() for b in bichos_escolhidos.split(",") if b.strip().title() in bichos_dict]

    milhares = []
    centenas = set()

    for milhar in pedras_milhar:
        for centena in pedras_centena:
            for bicho in bichos:
                for dezena in bichos_dict[bicho]:
                    milhar_completa = f"{milhar}{centena}{str(dezena).zfill(2)}"
                    centenas.add(f"{centena}{str(dezena).zfill(2)}")
                    milhares.append(milhar_completa)

    return milhares, sorted(centenas)

# Botão para gerar os resultados
if st.button("🎰 Gerar Milhares e Centenas"):
    milhares, centenas = gerar_milhares_centenas()

    if milhares:
        st.subheader("📌 Milhares Geradas:")
        st.text("\n".join(milhares))

    if centenas:
        st.subheader("📌 Centenas Geradas:")
        st.text("\n".join(centenas))

# Rodapé
st.markdown("---")
st.markdown("📌 **APS - O Melhor Analisador do Jogo do Bicho** 🔥")
