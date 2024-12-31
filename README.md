# instagram-bot
🤖🦾📸 Uma maneira automatizada de excluir o número de seguindos do Instagram.


## Bot

Vamos fazer uma consulta na classe responsável pela seção de seguindo (following) do perfil do Instagram:

```javascript
// Classe responsável pela seção de seguindo do perfil do Instagram
let seguindo = parseInt(document.getElementsByClassName('x5n08af x1s688f')[0]?.innerHTML || 0) // [2].innerHTML 
// seguindo[2] = divs HTML dessas classes
```

Após, todos esses estudos, criei o código da nossa aplicação final:

```javascript
let listaSeguidos = [];

function capturarSeguidos() {
    let elementos = document.getElementsByClassName('_ap3a _aaco _aacw _aacx _aad7 _aade');
    for (let element of elementos) {
        let nome = element.innerText.trim();
        if (!listaSeguidos.includes(nome)) {
            listaSeguidos.push(nome);
        }
    }
}

// Detecta alterações no DOM
let observer = new MutationObserver(capturarSeguidos);

observer.observe(document.body, {
    childList: true,
    subtree: true,
});

// Role a página automaticamente para carregar mais elementos
const rolarPagina = setInterval(() => {
    document.querySelector('._a6hd')?.scrollIntoView();
    if (listaSeguidos.length >= seguindo - 1) {
        clearInterval(rolarPagina);
        observer.disconnect();
        console.log('Lista de seguidos:', listaSeguidos);
    }
}, 3000);
```

## RPA - Robot Process Automation

```python
import pyautogui
import time
import webbrowser

# Lista de usernames a serem deixados de seguir
usuarios_a_remover = ["usuario1", "usuario2", "usuario3"]

# Configurações de tempo (ajuste conforme necessário)
TEMPO_ENTRE_ACOES = 2  # Tempo entre ações para evitar erros

# URL da página de "seguindo"
username = "SEU_USERNAME"  # Substitua pelo seu username
url_following = f"https://www.instagram.com/{username}/following/"

# Abrir navegador na página de "seguindo"
webbrowser.open(url_following)
time.sleep(5)  # Tempo para o navegador carregar a página

# Acessar a barra de busca e iterar pelos usuários
for usuario in usuarios_a_remover:
    try:
        # Clique na barra de busca na lista de "seguindo" (ajuste as coordenadas para sua tela)
        pyautogui.click(x=500, y=250)  # Coordenadas do campo de busca
        time.sleep(TEMPO_ENTRE_ACOES)

        # Digitar o nome do usuário
        pyautogui.write(usuario, interval=0.1)
        time.sleep(TEMPO_ENTRE_ACOES)

        # Localizar e clicar no botão "Seguindo" ao lado do nome (ajuste as coordenadas)
        pyautogui.click(x=600, y=300)  # Coordenadas do botão "Seguindo"
        time.sleep(TEMPO_ENTRE_ACOES)

        # Confirmar "Deixar de seguir"
        pyautogui.click(x=650, y=400)  # Coordenadas do botão de confirmação
        time.sleep(TEMPO_ENTRE_ACOES)

        print(f"Deixou de seguir {usuario}.")
    except Exception as e:
        print(f"Erro ao tentar deixar de seguir {usuario}: {e}")

print("Processo concluído.")
```
