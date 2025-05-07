# PLN

!python -m venv venv

!source venv/bin/activate

!pip install nltk spacy

# Explicação: Esses comandos funcionam apenas em Jupyter Notebook/Linux, não em scripts .py. Criam e ativam um ambiente virtual chamado venv. e instalam as bibliotecas NLTK e spaCy.

import nltk

import spacy

# (1) Carregar texto: string fixa ou arquivo

USE_FILE = False  # Altere para True se quiser carregar de um arquivo .txt

if USE_FILE:

    file_path = 'texto.txt'
    
    with open(file_path, 'r', encoding='utf-8') as f:
    
        texto = f.read()
else:

    texto = """python -m venv venv
    
source venv/bin/activate  # No Windows: venv\\Scripts\\activate

pip install nltk spacy """

# (2) Preparar NLTK

nltk.download('punkt')

# Download the 'punkt_tab' resource

nltk.download('punkt_tab') # This line was added to download the necessary resource

# Tokenizar com NLTK

tokens_nltk = nltk.word_tokenize(texto)

print("Tokens com NLTK:")

print(tokens_nltk)

# (3) Preparar spaCy

try:

    nlp = spacy.load("en_core_web_sm")
    
except OSError:

    print("Modelo 'en_core_web_sm' não encontrado. Execute no terminal:")
    
    print("python -m spacy download en_core_web_sm")
    
    exit()

# Tokenizar com spaCy

doc = nlp(texto)

tokens_spacy = [token.text for token in doc]

print("\nTokens com spaCy:")

print(tokens_spacy)

##

import re

text = "A Sra. Rosa plantou uma rosa no jardim. O céu estava azul e a brisa era suave."

tokens = re.findall(r'\w+', text.lower())

print(tokens)

import re

text = "A Sra. Rosa plantou uma rosa no jardim. O céu estava azul e a brisa era suave."

clean_text = re.sub(r'[^\w\s]', '', text).lower()

print(clean_text)

# Explicação: Remove pontuação e converte tudo para minúsculas. Depois divide em tokens simples com split() ou re.findall().

!pip install nltk

import nltk

nltk.download('stopwords')

from nltk.corpus import stopwords

stop_words = set(stopwords.words('portuguese'))

filtered_tokens = [word for word in tokens if word not in stop_words]
# Explicação: Baixa e aplica a lista de stopwords em português (ex: "a", "e", "o", "no"). Remove essas palavras dos tokens.

from nltk import ngrams

bigrams = list(ngrams(filtered_tokens, 2))

trigrams = list(ngrams(filtered_tokens, 3))
# Explicação: Gera pares (bigrams) e trios (trigrams) de palavras consecutivas do texto filtrado.

!pip install spacy

!python -m spacy download pt_core_news_sm

import spacy

nlp = spacy.load('pt_core_news_sm')

doc = nlp(" ".join(filtered_tokens))

lemmatized = [token.lemma_ for token in doc]

print(lemmatized)
# Explicação: Usa o modelo português do spaCy. Lematiza as palavras, ou seja, reduz para sua forma canônica: Ex: "plantou" → "plantar", "rosas" → "rosa".
