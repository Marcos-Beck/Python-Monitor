## Monitor Python

Monitor de arquivos Python com reinicialização automática do programa quando arquivos monitorados são modificados, criados, excluídos ou renomeados.

**Importante: os códigos abaixo são exemplos e podem ser adaptados conforme necessário.**

### 1. Inicialização

**Abrir o monitor com seleção interativa do arquivo:**

```bash
py monitor.py
```

**Executar diretamente um arquivo específico:**

```bash
py monitor.py teste_monitor.py
```

Também é possível informar o caminho relativo:

```bash
py monitor.py modules/main.py
```

### 2. Monitoramento de diretórios

**Monitorar todo o projeto (padrão):**

```bash
py monitor.py teste_monitor.py
```

**Monitorar um diretório específico:**

```bash
py monitor.py teste_monitor.py --watch modules
```

**Monitorar vários diretórios:**

```bash
py monitor.py teste_monitor.py --watch modules --watch projects
```

O monitoramento é recursivo, incluindo as subpastas dos diretórios selecionados.

### 3. Ignorar arquivos e pastas

**Ignorar uma pasta:**

```bash
py monitor.py teste_monitor.py --ignore test
```

**Ignorar um arquivo específico:**

```bash
py monitor.py teste_monitor.py --ignore auxiliar.py
```

**Ignorar arquivos por extensão ou padrão:**

```bash
py monitor.py teste_monitor.py --ignore "*.log"
```

**Ignorar vários arquivos ou pastas:**

```bash
py monitor.py teste_monitor.py --ignore test --ignore "*.log" --ignore arquivo.py
```

O monitor já ignora automaticamente algumas pastas:

- `.git`
- `.venv`
- `venv`
- `env`
- `__pycache__`
- `build`
- `dist`
- `.pytest_cache`

### 4. Reativar arquivos e pastas ignorados

O parâmetro `--unignore` cria uma exceção às regras de exclusão.

**Reativar uma pasta:**

```bash
py monitor.py teste_monitor.py --ignore test --unignore test
```

**Reativar um arquivo:**

```bash
py monitor.py teste_monitor.py --ignore "*.py" --unignore auxiliar.py
```

As exceções têm prioridade sobre as regras de exclusão, inclusive sobre as pastas ignoradas automaticamente.

### 5. Configurar o tempo de reinicialização

O parâmetro `--debounce` define o intervalo de espera após a última alteração detectada, evitando reinicializações repetidas durante um mesmo salvamento.

**Usar o padrão (0,6 segundo):**

```bash
py monitor.py teste_monitor.py
```

**Definir 1 segundo:**

```bash
py monitor.py teste_monitor.py --debounce 1
```

**Definir 2 segundos:**

```bash
py monitor.py teste_monitor.py --debounce 2
```

O valor mínimo aceito é de 0,1 segundo.

### 6. Consultar os comandos disponíveis

```bash
py monitor.py --help
```

### 7. Encerrar o monitor

Pressione:

```text
CTRL + C
```

O monitor interromperá a execução do programa e encerrará o processo de monitoramento.

---

### Resumo dos parâmetros

| Parâmetro | Função |
|---|---|
| `arquivo` | Define o script Python que será executado |
| `-w`, `--watch` | Define os diretórios monitorados |
| `-i`, `--ignore` | Define arquivos e pastas ignorados |
| `-u`, `--unignore` | Cria exceções às regras de exclusão |
| `--debounce` | Define o intervalo para reinicialização |
| `-h`, `--help` | Exibe a ajuda do monitor |

**Observação:** 
- Ao modificar o próprio `monitor.py`, é necessário encerrar e iniciar novamente o terminal para carregar a nova versão do monitor.
- O monitor só funciona com arquivos Python (.py).