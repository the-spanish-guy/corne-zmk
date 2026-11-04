# Corne Wireless com ZMK

A configuração do meu Corne sem fio (split, 3x6 + 3 teclas de polegar), feita para escrever em português e programar com conforto. O firmware é compilado pelo GitHub Actions: você muda um arquivo, dá push, e uns minutos depois os arquivos prontos para gravar estão na aba **Actions**. Não precisa instalar nada no computador.

## Sumário
- [O que tem aqui](#o-que-tem-aqui)
- [Como instalar o firmware](#como-instalar-o-firmware)
- [Layers e layout](#layers-e-layout)
- [Combos e atalhos](#combos-e-atalhos)
- [Escrevendo em português](#escrevendo-em-português)
- [Bateria](#bateria)
- [Mudando a configuração](#mudando-a-configuração)
- [Se algo der errado](#se-algo-der-errado)
- [Créditos](#créditos)

## O que tem aqui

**Hardware**
- Teclado: Corne sem fio, com duas metades que se falam por Bluetooth
- Controladores: Nice!Nano v2 (um em cada metade)
- Telas: OLED de 128x32 nas duas metades. O nice!view também está no projeto, mas ainda **não foi testado** nesta versão do ZMK
- LEDs RGB: um por tecla, mais alguns de underglow, todos na mesma fita
- Baterias: uma 18650 de 3450 mAh em cada lado

**Software**
- 4 layers
- Teclas de modificador na linha do meio (segurar o `A`, `S`, `D`, `F`, `J`, `K` ou `L` vira Ctrl, Alt, Shift ou Win)
- Combos para símbolos e acentos
- Telas OLED com animações (gato, Luna e outras), por meio do módulo `zmk-nice-oled`
- Controle de Bluetooth (4 perfis), de mídia e do RGB direto no teclado
- ZMK Studio no lado esquerdo, para editar o keymap sem recompilar

## Como instalar o firmware

### 1. Baixar os arquivos
1. Abra a aba **Actions** do repositório e entre na última execução com o ícone verde.
2. No fim da página, baixe o artefato **firmware** (é um `.zip`) e descompacte.
3. Dentro dele há um arquivo para cada lado. Os nomes mudam conforme a tela que você usa:

| Para o OLED | Para o nice!view |
|---|---|
| `corne_left nice_oled-nice_nano__zmk-zmk.uf2` | `corne_left nice_view_adapter nice_view_gem-nice_nano__zmk-zmk.uf2` |
| `corne_right nice_oled-nice_nano__zmk-zmk.uf2` | `corne_right nice_view_adapter nice_view_gem-nice_nano__zmk-zmk.uf2` |

E um arquivo de limpeza, usado só quando algo dá errado: `settings_reset-nice_nano__zmk-zmk.uf2`.

### 2. Gravar em cada lado
1. Ligue a metade no computador pelo USB.
2. Aperte o botão de **reset duas vezes rápido**. Uma unidade chamada `NICENANO` aparece no computador.
3. Copie o arquivo `.uf2` certo (esquerdo ou direito) para essa unidade.
4. Espere a unidade sumir sozinha. Isso quer dizer que terminou.
5. Repita com a outra metade.

**Dica:** na primeira vez, ou depois de uma mudança grande, grave primeiro o `settings_reset` em **cada lado** e só depois o firmware normal. Isso apaga pareamentos e configurações antigas, e evita muita dor de cabeça. Depois, você precisa parear o teclado de novo com o computador ou o celular.

### 3. Primeiro uso
- O lado **esquerdo** é o que se liga ao computador. Use o USB nele quando quiser digitar com cabo.
- O lado **direito** se conecta ao esquerdo sozinho, e a tela dele mostra um check quando isso acontece.
- O cabo TRRS entre as metades não é usado para comunicação: as duas conversam por Bluetooth.

## Layers e layout

O teclado tem 4 layers (camadas). A principal é a 0, e as outras você acessa segurando uma tecla de polegar.

```mermaid
graph TD
    A[Layer 0 - Letras] -->|segurar a tecla do meio do polegar esquerdo| B[Layer 1 - Números e símbolos]
    A -->|segurar Enter, ou a tecla do meio da direita| C[Layer 2 - Navegação]
    A -->|segurar Espaço| D[Layer 3 - Bluetooth, F1 a F12, mídia e RGB]
```

Nos desenhos abaixo, um ponto (`·`) é uma tecla que não faz nada de novo naquela layer e usa a da layer de baixo. Um `A·GUI` quer dizer "toque para A, segure para Win".

### Layer 0: letras (base)

```
,-------+-------+-------+-------+-------+-------.     ,-------+-------+-------+-------+-------+-------.
|  TAB  |   Q   |   W   |   E   |   R   |   T   |     |   Y   |   U   |   I   |   O   |   P   | BKSP  |
|-------+-------+-------+-------+-------+-------|     |-------+-------+-------+-------+-------+-------|
| CTRL  | A·GUI | S·ALT | D·CTL | F·SFT |   G   |     |   H   | J·SFT | K·CTL | L·ALT |   ;   |   '   |
|-------+-------+-------+-------+-------+-------|     |-------+-------+-------+-------+-------+-------|
| SHIFT |   Z   |   X   |   C   |   V   |   B   |     |   N   |   M   |   ,   |   .   |   /   |  ESC  |
`-------+-------+-------+-------+-------+-------'     `-------+-------+-------+-------+-------+-------'
                        |  WIN  |  L1   |ENT·L2 |     |ESP·L3 |  L2   |  ALT  |
                        `-----------------------'     `-----------------------'
```

Nos polegares:
- **Esquerda:** Win, `L1` (segurar abre a layer 1), `Enter` (toque) ou layer 2 (segurar)
- **Direita:** `Espaço` (toque) ou layer 3 (segurar), `L2` (segurar abre a layer 2), Alt

### Layer 1: números e símbolos

```
,-------+-------+-------+-------+-------+-------.     ,-------+-------+-------+-------+-------+-------.
|   `   |   1   |   2   |   3   |   4   |   5   |     |   6   |   7   |   8   |   9   |   0   | BKSP  |
|-------+-------+-------+-------+-------+-------|     |-------+-------+-------+-------+-------+-------|
|   ·   | RGB ON|RGB OFF|   ·   |   ·   |  F12  |     |   -   |   =   |   `   |   ·   |   '   |   ·   |
|-------+-------+-------+-------+-------+-------|     |-------+-------+-------+-------+-------+-------|
|   ·   |EXT PWR|   ·   |   ·   |   [   |   ]   |     |   ·   |   ·   |   ·   |   ·   |   \   |   ·   |
`-------+-------+-------+-------+-------+-------'     `-------+-------+-------+-------+-------+-------'
                        |   ·   |   ·   |   ·   |     |   ·   | SHIFT |   ·   |
                        `-----------------------'     `-----------------------'
```

`EXT PWR` liga e desliga a alimentação externa dos LEDs. `RGB ON` e `RGB OFF` ligam e desligam o efeito.

### Layer 2: navegação e teclado numérico

```
,-------+-------+-------+-------+-------+-------.     ,-------+-------+-------+-------+-------+-------.
|   ·   |  ESC  |   7   |   8   |   9   |   0   |     | HOME  |   ·   |   ↑   |   ·   |   ·   |   ·   |
|-------+-------+-------+-------+-------+-------|     |-------+-------+-------+-------+-------+-------|
|   ·   | CAPS  |   4   |   5   |   6   |   @   |     |  END  |   ←   |   ↓   |   →   |   ·   |   ·   |
|-------+-------+-------+-------+-------+-------|     |-------+-------+-------+-------+-------+-------|
|   ·   |  DEL  |   1   |   2   |   3   |   .   |     |   ·   |   ·   |   ·   |   ·   |   ·   |   ·   |
`-------+-------+-------+-------+-------+-------'     `-------+-------+-------+-------+-------+-------'
```

### Layer 3: Bluetooth, funções, mídia e RGB

```
,-------+-------+-------+-------+-------+-------.     ,-------+-------+-------+-------+-------+-------.
|   ·   |  BT 1 |  BT 2 |  BT 3 |  BT 4 | BT CLR|     |  F1   |  F2   |  F3   |  F4   |  F5   |  F6   |
|-------+-------+-------+-------+-------+-------|     |-------+-------+-------+-------+-------+-------|
|   ·   |RGB LIG|RGB EFE|RGB BRI|RGB BRD|RGB VEL|     |  F7   |  F8   |  F9   |  F10  |  F11  |  F12  |
|-------+-------+-------+-------+-------+-------|     |-------+-------+-------+-------+-------+-------|
|   ·   | ANTER | PLAY  | PRÓX  | VOL - | VOL + |     |   ·   |   ·   |   ·   |   ·   |   ·   |   ·   |
`-------+-------+-------+-------+-------+-------'     `-------+-------+-------+-------+-------+-------'
```

- `BT 1` a `BT 4` escolhem com qual aparelho o teclado fala (4 perfis). `BT CLR` apaga o pareamento do perfil atual.
- `RGB LIG` liga e desliga o RGB, `RGB EFE` troca o efeito, `RGB BRI` e `RGB BRD` aumentam e diminuem o brilho, `RGB VEL` muda a velocidade.

## Combos e atalhos

Um **combo** é apertar duas teclas ao mesmo tempo para fazer outra coisa. Aqui, as duas teclas precisam ser apertadas quase juntas (em menos de 50 milissegundos).

| Teclas juntas | Resultado | Para quê |
|---|---|---|
| `Q` + `W` | Esc | Sair de modos e fechar janelas |
| `E` + `D` | ç | Cedilha |
| `A` + `S` | tap dance do `A` | Acentos (veja abaixo). Experimental |
| `R` + `E` | `[` | Colchete esquerdo |
| `U` + `I` | `]` | Colchete direito |
| `D` + `F` | `(` | Parêntese esquerdo |
| `J` + `K` | `)` | Parêntese direito |
| `C` + `V` | `{` | Chave esquerda |
| `,` + `M` | `}` | Chave direita |
| `T` + `Y` | `\` | Barra invertida |
| `G` + `H` | `\|` | Pipe, comum no terminal |

> Os colchetes e o `\` também estão na layer 1, caso você prefira digitar assim.

## Escrevendo em português

**Acentos com toque repetido (tap dance):** no `A` e no `E`, tocar uma, duas ou três vezes seguidas dá versões diferentes da letra. O segundo toque usa a tecla **AltGr** e o terceiro usa **AltGr com Shift**, então o que aparece depende do layout do teclado do seu sistema (por exemplo, "US Internacional"). Se não sair o acento que você espera, ajuste o layout do sistema.

**Macro `cao`:** digita as teclas C, A, O e um til por AltGr. Também depende do layout do sistema.

O `ç` tem um combo próprio: aperte `E` e `D` juntos.

## Bateria

- **Display:** apaga sozinho quando você para de digitar.
- **RGB:** desliga no idle e volta quando você digita de novo. Pode ser que o lado que você usa menos apague antes do outro.
- **Idle:** 2 minutos sem tocar nas teclas. **Deep sleep:** 30 minutos. Ao acordar do deep sleep, o teclado pode levar alguns segundos para reconectar.
- **Potência do Bluetooth:** 0 dBm. Se o teclado ficar perdendo conexão com o computador, aumente para +4 ou +8 no arquivo `config/corne.conf`.

**A porcentagem da bateria mente um pouco.** O ZMK calcula o número olhando a tensão da bateria, e a tensão cai quando o teclado está sob carga (RGB, tela, Bluetooth). Por isso o número pode cair uns pontos logo depois de ligar e voltar a subir sozinho. Para ver quanto de bateria sobrou de verdade, olhe o número com o teclado parado, depois de uns 2 minutos.

## Mudando a configuração

| Arquivo | Para quê |
|---|---|
| `config/corne.keymap` | O layout: teclas, layers, combos, macros |
| `config/corne.conf` | Opções das **duas** metades: tela, RGB, bateria, sleep e Bluetooth |
| `config/boards/shields/corne/corne_left.conf` | Só do lado esquerdo (ZMK Studio) |
| `config/boards/shields/corne/corne_right.conf` | Só do lado direito (hoje vazio) |
| `build.yaml` | Quais firmwares a Action compila (OLED, nice!view e o de limpeza) |
| `config/west.yml` | Versão do ZMK e dos módulos de tela |
| `config/boards/shields/corne/` | A descrição do hardware do Corne (pinos, matriz, LEDs, OLED) |

**Fluxo normal:** mude o arquivo, dê commit e push, espere a Action ficar verde e baixe o firmware.

A Action roda sozinha quando algo dentro da pasta `config/` muda. Se você mudar **só o `build.yaml`**, ela não dispara: vá na aba Actions e use **Run workflow**.

### Opções que você provavelmente vai querer mexer

**Brilho do RGB** (no `corne.conf`):
```
CONFIG_ZMK_RGB_UNDERGLOW_BRT_START=30   # brilho ao ligar (%)
CONFIG_ZMK_RGB_UNDERGLOW_BRT_MAX=60     # brilho máximo (%)
CONFIG_ZMK_RGB_UNDERGLOW_EFF_START=3    # efeito ao ligar
```

**Tempo de idle e sleep** (em milissegundos):
```
CONFIG_ZMK_IDLE_TIMEOUT=120000          # 2 minutos
CONFIG_ZMK_IDLE_SLEEP_TIMEOUT=1800000   # 30 minutos (precisa ser maior que o idle)
```

**Animações do OLED:** no `corne.conf` há uma lista de todas as animações do módulo `zmk-nice-oled`, comentadas e com uma explicação de cada uma. Tire o `#` da que quiser.

## Se algo der errado

### O teclado trava uns 2 segundos depois de ligar, e as telas congelam
Isso aconteceu quando o módulo da tela OLED recebia pouca memória. A correção está no `corne.conf`:
```
CONFIG_ZMK_DISPLAY_DEDICATED_THREAD_STACK_SIZE=8192
```
**Não diminua esse valor.** Com 3072 (o que o ZMK usa por padrão), o teclado trava.

### O Bluetooth não conecta, ou o lado direito não acha o esquerdo
1. No computador ou celular, remova o "Corne" da lista de aparelhos Bluetooth.
2. Grave o `settings_reset` nos **dois** lados.
3. Grave o firmware normal em cada lado (os dois, com a mesma versão).
4. Ligue os dois e pareie o teclado de novo.

### A tela do OLED está mostrando só pontinhos aleatórios
Costuma ser o que uma tela OLED mostra quando o firmware não a inicializou (ou travou no meio de uma atualização). Se continuar assim depois de gravar o firmware normal, confira se gravou o arquivo certo (o do `nice_oled`) e veja o item sobre o teclado travar, logo acima.

### A Action falhou
Abra a execução com o X vermelho, clique no job que falhou e leia a última parte do log. Os erros mais comuns são uma opção de configuração que não existe mais (o Kconfig reclama de um símbolo indefinido) e um módulo de tela que ainda não funciona com a versão atual do ZMK.

## Créditos

- [ZMK Firmware](https://zmk.dev)
- [Corne Keyboard, foostan/crkbd](https://github.com/foostan/crkbd)
- Config base: [ZMK Config](https://github.com/zmkfirmware/zmk-config)
- Telas OLED: [zmk-nice-oled](https://github.com/mctechnology17/zmk-nice-oled), com a migração para o ZMK atual feita em [tokyo2006/zmk-nice-oled](https://github.com/tokyo2006/zmk-nice-oled)
- Tela nice!view: [nice-view-gem](https://github.com/M165437/nice-view-gem)

---

Feito por [the spanish guy](https://github.com/the-spanish-guy) com :black_heart:

```
          ／＞　 フ
         | 　_　_|
       ／` ミ__^ノ
      /　　　　 |
     /　 ヽ　　 ﾉ           ╱|、
    /　　 |　|　|         (˚ˎ 。7
／￣|　　 |　|　|          |、˜〵
(￣ヽ＿_  ヽ_)__)         じしˍ,)ノ
＼二)
```
