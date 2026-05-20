# Guia de Hospedagem — Mapa DPDF
**GitHub Pages + Netlify — Passo a passo completo**

---

## Visão geral da arquitetura

```
GitHub (repositório)
  ├── data.json          ← você edita aqui para atualizar comarcas/dados
  └── mapa-defensoria-dpdf.html

Netlify (hospedagem gratuita)
  └── lê o repositório do GitHub e publica o site automaticamente
```

Toda vez que você editar o `data.json` no GitHub, o Netlify republica o site em segundos.

---

## PARTE 1 — Criar conta e repositório no GitHub

**1.** Acesse **github.com** e clique em **Sign up** (crie uma conta gratuita)

**2.** Após entrar, clique no botão verde **New** (canto superior esquerdo) para criar um repositório

**3.** Preencha:
- **Repository name:** `mapa-dpdf` (ou o nome que preferir)
- **Visibility:** ✅ **Public** (obrigatório para o Netlify gratuito funcionar)
- Clique em **Create repository**

**4.** Na página do repositório vazio, clique em **uploading an existing file**

**5.** Arraste os dois arquivos para a área de upload:
- `mapa-defensoria-dpdf.html`
- `data.json`

**6.** Clique em **Commit changes** (botão verde)

---

## PARTE 2 — Obter a URL raw do data.json

**1.** No repositório, clique no arquivo `data.json`

**2.** Clique no botão **Raw** (canto superior direito do arquivo)

**3.** Copie a URL da barra de endereços. Ela terá este formato:
```
https://raw.githubusercontent.com/SEU_USUARIO/mapa-dpdf/main/data.json
```

**4.** De volta no repositório, clique em `mapa-defensoria-dpdf.html` → botão **Edit** (ícone de lápis ✏️)

**5.** Use **Ctrl+F** para encontrar o texto:
```
DATA_URL_PLACEHOLDER
```

**6.** Substitua pelo endereço raw que você copiou:
```javascript
const DATA_URL = 'https://raw.githubusercontent.com/SEU_USUARIO/mapa-dpdf/main/data.json';
```

**7.** Clique em **Commit changes**

---

## PARTE 3 — Hospedar no Netlify

**1.** Acesse **netlify.com** → clique em **Sign up** → escolha **Sign up with GitHub** (usa a mesma conta)

**2.** No painel do Netlify, clique em **Add new site → Import an existing project**

**3.** Clique em **Deploy with GitHub**

**4.** Autorize o Netlify a acessar sua conta GitHub

**5.** Selecione o repositório `mapa-dpdf`

**6.** Na tela de configuração, deixe tudo padrão e clique em **Deploy site**

**7.** Aguarde ~1 minuto. O Netlify vai gerar uma URL como:
```
https://wonderful-name-123456.netlify.app
```

**8.** (Opcional) Para personalizar a URL: **Site configuration → Site details → Change site name**
   - Exemplo: `mapa-dpdf.netlify.app`

---

## PARTE 4 — Como atualizar os dados futuramente

### Atualizar comarcas ou dados bancários

**1.** Acesse **github.com** → seu repositório `mapa-dpdf`

**2.** Clique em `data.json` → botão **Edit** (lápis ✏️)

**3.** Edite o arquivo. Exemplos:

**Adicionar uma comarca:**
```json
"GOIÁS": [
  {"nome": "Goiânia", "tem": true},
  {"nome": "Aparecida de Goiânia", "tem": true},
  {"nome": "Nova cidade aqui", "tem": false}
]
```

**Atualizar conta bancária:**
```json
"GOIÁS": {
  "fundo": "Nome do Fundo",
  "banco": "Banco do Brasil (001)",
  "agencia": "1234-5",
  "conta": "67890-1",
  "pedido": "texto completo do pedido..."
}
```

**4.** Clique em **Commit changes**

**5.** O Netlify detecta a mudança e republica o site em ~30 segundos ✅

---

## Estrutura do data.json (referência)

```json
{
  "sucumbencia": {
    "NOME DO ESTADO": {
      "fundo": "Nome do fundo",
      "cnpj": "00.000.000/0001-00",
      "banco": "Banco do Brasil (001)",
      "agencia": "0000-0",
      "conta": "00000-0",
      "pedido": "texto do parágrafo de pedido..."
    }
  },
  "comarcas": {
    "NOME DO ESTADO": [
      {"nome": "Nome da Comarca", "tem": true},
      {"nome": "Outra Comarca", "tem": false}
    ]
  },
  "nomeacao_padrao": "texto padrão do parágrafo de nomeação...",
  "nomeacao_custom": {
    "NOME DO ESTADO": "texto personalizado para este estado"
  }
}
```

---

## Resumo das URLs após configuração

| O quê | URL |
|---|---|
| Repositório GitHub | `github.com/SEU_USUARIO/mapa-dpdf` |
| Site publicado | `mapa-dpdf.netlify.app` |
| Dados (raw) | `raw.githubusercontent.com/SEU_USUARIO/mapa-dpdf/main/data.json` |

---

*Desenvolvido por Gustavo Freitas de Souza — Servidor DPDF/SEMED · 2026*
