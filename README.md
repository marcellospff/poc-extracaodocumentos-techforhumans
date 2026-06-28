# POC: Extração de Documentos com IA Generativa

Prova de Conceito desenvolvida para o Desafio Técnico de Estágio em Pesquisa e Desenvolvimento em IA Generativa da **Tech for Humans**.

Demonstra a **Abordagem C, Pipeline Híbrida Modular**, recomendada no Dossiê de Pesquisa, implementada com Google Gemini 2.5 Flash via API REST.

---

## Casos de Uso

| Caso | Documento | Objetivo |
|---|---|---|
| 1 | CNH | Extrair campos predeterminados (Nome, CPF, Data de Nascimento, Data de Emissão, Filiação Pai, Filiação Mãe) |
| 2 | Paper Claude 3 (42 páginas) | Extrair conteúdo para texto mantendo layout, tabelas e interpretação de gráficos |
| 3 | Fatura de Energia CELPE | Extrair conteúdo completo mantendo organização hierárquica das informações |

---

## Estrutura do Repositório

```
.
├── POC_TechForHumans_Marcello_Siqueira.ipynb   # Notebook principal
├── README.md                                    # Este arquivo
```

Os documentos utilizados nos casos de uso (CNH, fatura e paper) não estão incluídos no repositório por questões de privacidade. Substitua pelos documentos equivalentes conforme descrito na seção de configuração abaixo.

---

## Requisitos

- Python 3.10 ou superior
- Conta no [Google AI Studio](https://aistudio.google.com) com chave de API gratuita
- Poppler instalado (necessário para o `pdf2image` converter o PDF em imagens)

### Instalação do Poppler

**Windows:** baixe em [github.com/oschwartz10612/poppler-windows/releases](https://github.com/oschwartz10612/poppler-windows/releases), extraia e adicione o caminho `...\poppler\Library\bin` à variável de ambiente PATH.

**Mac:**
```bash
brew install poppler
```

**Linux:**
```bash
sudo apt install poppler-utils
```

---

## Como Rodar

**1.** Clone o repositório:
```bash
git clone https://github.com/seu-usuario/poc-extracaodocumentos-techforhumans.git
cd poc-extracaodocumentos-techforhumans
```

**2.** Instale as dependências:
```bash
pip install pdf2image Pillow requests jupyter
```

**3.** Adicione os documentos na mesma pasta do notebook:
```
Documento 1.jpeg   (CNH)
Documento 2.jpg    (Fatura de Energia)
Documento 3.pdf    (Paper Claude 3 Model Family)
```

**4.** Abra o notebook:
```bash
jupyter notebook POC_TechForHumans_Marcello_Siqueira.ipynb
```

**5.** Na segunda célula, insira sua chave da API do Google AI Studio:
```python
GOOGLE_API_KEY = "SUA_CHAVE_AQUI"
```

**6.** Execute todas as células em sequência: **Kernel → Restart & Run All**

> O Caso 2 processa 42 páginas em lotes e pode levar entre 5 e 10 minutos dependendo da velocidade da conexão.

---

## Sobre a Implementação

A POC utiliza chamadas HTTP diretas à API REST do Gemini, sem dependência de bibliotecas cliente proprietárias, o que garante compatibilidade com qualquer ambiente Python 3.10+.

O schema JSON de cada caso de uso é incluído diretamente no prompt, e o modelo retorna um objeto JSON estruturado em uma única inferência, eliminando a segunda chamada de formatação do pipeline atual.

O Caso 2 implementa processamento em lotes de 6 páginas por chamada, demonstrando como a solução lidaria com documentos extensos em produção.

---

## Autor

**Marcello Siqueira**
Pesquisador de IA Generativa (P&D)
Desafio Técnico, Tech for Humans, junho de 2026