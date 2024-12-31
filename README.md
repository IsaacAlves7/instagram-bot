# instagram-bot
🤖🦾📸 Instagram bot from scratch.


## Bot
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

## RPA

```python
import pyautogui
import time

# Lista de usernames a serem deixados de seguir
usuarios_a_remover = ["usuario1", "usuario2", "usuario3"]

# Configurações de tempo (ajuste conforme necessário)
TEMPO_ENTRE_ACOES = 2  # Tempo entre ações para evitar erros

# Abrir navegador e acessar Instagram manualmente antes de executar o script
print("Certifique-se de que o Instagram está aberto e no perfil correto.")

time.sleep(5)  # Tempo para ajustar o navegador

# Navega pela lista de usuários e realiza as ações
for usuario in usuarios_a_remover:
    try:
        # Clique na barra de busca na lista de "seguindo" (ajuste as coordenadas para sua tela)
        pyautogui.click(x=100, y=200)  # Coordenadas do campo de busca
        time.sleep(TEMPO_ENTRE_ACOES)

        # Digitar o nome do usuário
        pyautogui.write(usuario, interval=0.1)
        time.sleep(TEMPO_ENTRE_ACOES)

        # Localizar e clicar no botão "Seguindo" ao lado do nome (ajuste as coordenadas)
        pyautogui.click(x=150, y=300)  # Coordenadas do botão "Seguindo"
        time.sleep(TEMPO_ENTRE_ACOES)

        # Confirmar "Deixar de seguir"
        pyautogui.click(x=200, y=350)  # Coordenadas do botão de confirmação
        time.sleep(TEMPO_ENTRE_ACOES)

        print(f"Deixou de seguir {usuario}.")
    except Exception as e:
        print(f"Erro ao tentar deixar de seguir {usuario}: {e}")

print("Processo concluído.")
```
