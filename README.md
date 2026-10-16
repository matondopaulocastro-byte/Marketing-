# Guia Completo: Como Utilizar a Biblioteca Pillow em Python

A **Pillow** (PIL Fork) é a biblioteca mais popular em Python para processamento, edição e criação de imagens do zero. Este guia prático ensina as principais operações passo a passo.

---

## 1. Instalação e Configuração

Para instalar a Pillow na sua máquina ou ambiente Linux/iSH, execute o comando correspondente:

### No Windows/macOS/Linux Padrão:
```bash
pip install Pillow
```

### No iSH Shell (Alpine Linux):
Antes do pip, instale as dependências de sistema C para evitar erros de compilação:
```bash
apk update && apk add jpeg-dev zlib-dev freetype-dev gcc musl-dev python3-dev
pip3 install Pillow
```

---

## 2. Operações Básicas com Imagens

O módulo principal da biblioteca é o `Image`. Com ele, pode abrir, criar, modificar e salvar arquivos.

### Abrir, Consultar Dados e Salvar
```python
from PIL import Image

# Abrir uma imagem existente
img = Image.open("foto.jpg")

# Consultar metadados básicos
print("Formato:", img.format)  # Ex: JPEG, PNG
print("Tamanho (Largura, Altura):", img.size)
print("Modo de cor:", img.mode)  # Ex: RGB, RGBA, L (Escala de cinzas)

# Salvar a imagem noutro formato (Conversão automática)
img.save("nova_foto.png")
```

### Criar uma Imagem do Zero
Pode gerar uma tela em branco definindo o modo de cor, as dimensões e uma cor sólida de fundo:
```python
# Cria uma imagem RGB de 500x500 pixels totalmente vermelha
img_nova = Image.new("RGB", (500, 500), color="red")
img_nova.save("quadrado_vermelho.png")
```

---

## 3. Manipulação e Transformações

### Redimensionar (Resize) e Cortar (Crop)
```python
# Redimensionar para 200x200 pixels
img_redimensionada = img.resize((200, 200))
img_redimensionada.save("foto_pequena.jpg")

# Cortar uma região da imagem (Coordenadas: Esquerda, Cima, Direita, Baixo)
caixa_corte = (100, 100, 400, 400)
img_cortada = img.crop(caixa_corte)
img_cortada.save("foto_cortada.jpg")
```

### Rotacionar e Inverter
```python
# Rotacionar 90 graus no sentido anti-horário
img_rodada = img.rotate(90)

# Inverter horizontalmente (Espelhar)
img_espelhada = img.transpose(Image.FLIP_LEFT_RIGHT)
```

---

## 4. Desenhar Elementos Gráficos e Texto

Para desenhar formas geométricas ou escrever mensagens em cima de uma imagem, utilizamos o módulo `ImageDraw`.

```python
from PIL import Image, ImageDraw, ImageFont

# Criar uma base branca
fundo = Image.new("RGB", (600, 400), "white")
desenho = ImageDraw.Draw(fundo)

# 1. Desenhar uma Linha (Pontos iniciais e finais, cor, espessura)
desenho.line([(50, 50), (550, 50)], fill="black", width=5)

# 2. Desenhar um Retângulo
desenho.rectangle([(50, 100), (250, 250)], fill="blue", outline="red", width=3)

# 3. Desenhar uma Elipse / Círculo
desenho.ellipse([(350, 100), (550, 250)], fill="green")

# 4. Escrever Texto (Sem fonte externa)
desenho.text((50, 300), "Texto Padrão (Sem Fonte)", fill="black")

# 5. Escrever Texto com Fonte Personalizada (Ex: Arial .ttf)
try:
    # Substitua pelo caminho de uma fonte válida no seu sistema
    fonte = ImageFont.truetype("arial.ttf", size=24)
    desenho.text((50, 340), "Texto Estilizado", fill="purple", font=fonte)
except IOError:
    print("Aviso: Arquivo de fonte não encontrado. Usando texto padrão.")

fundo.save("desenho_final.png")
```

---

## 5. Aplicar Filtros e Efeitos

O módulo `ImageFilter` permite desfocar, realçar contornos e aplicar outros efeitos com apenas uma linha de código.

```python
from PIL import Image, ImageFilter

img_original = Image.open("foto.jpg")

# Aplicar efeito de Desfoque Gaussiano (Blur)
img_desfocada = img_original.filter(ImageFilter.GaussianBlur(radius=5))
img_desfocada.save("foto_blur.jpg")

# Encontrar Contornos da imagem (Efeito desenho)
img_contornos = img_original.filter(ImageFilter.CONTOUR)
img_contornos.save("foto_contornos.jpg")
```

---

## Dica de Ouro para o iSH Shell (iOS)
Como o ambiente de terminal no iOS não possui monitor ou interface visual imediata, lembre-se sempre de copiar os arquivos gerados pelo script para o diretório `/root/` ou uma pasta compartilhada para os visualizar através da aplicação **Ficheiros (Files)** do seu iPhone ou iPad:
```bash
cp desenho_final.png /root/
```