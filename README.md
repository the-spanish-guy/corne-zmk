# Configuração ZMK para Corne Wireless

Este é um fork personalizado da configuração ZMK para o teclado Corne Wireless, otimizado para uso em português e com várias melhorias de qualidade de vida.

## Hardware Suportado

- Controlador: Nice!Nano v2
- Display: Suporte para OLED e Nice!View
- RGB Underglow (opcional)
- Switches: Suporte para qualquer switch MX

## Características

- Layout otimizado para português com suporte a acentos
- 4 layers com funções específicas
- Combos intuitivos para caracteres especiais
- Tap dance para acentuação
- Macros para palavras comuns
- Controles de mídia e RGB
- Otimizações de energia para maior duração da bateria

## Layers

### Layer Base (0)
- Layout QWERTY padrão
- Modificadores nas teclas home row
- Acesso aos outros layers através de hold

### Layer Lower (1)
- Números
- Símbolos básicos
- Controles do sistema

### Layer Raise (2)
- Teclado numérico
- Navegação (setas)
- Controles do cursor

### Layer Funções (3)
- Controles Bluetooth
- Teclas de função (F1-F12)
- Controles de mídia
- Ajustes RGB

## Combos

- `Q + W` = ESC
- `K + L` = Enter
- `E + D` = Ç
- `[ ]` = Colchetes
- `( )` = Parênteses
- `{ }` = Chaves
- `\ |` = Barra invertida e Pipe

## Tap Dance

- `A` = a → á → â
- `E` = e → é → ê

## Como Compilar

1. Fork este repositório
2. Faça suas modificações (opcional)
3. A GitHub Action irá compilar automaticamente
4. Baixe os arquivos .uf2 gerados

## Como Flashear

1. Pressione o botão reset duas vezes no Nice!Nano
2. O teclado aparecerá como dispositivo USB "NICENANO"
3. Copie o arquivo .uf2 correspondente:
   - `corne_left_xxx-nice_nano_v2-zmk.uf2` para o lado esquerdo
   - `corne_right_xxx-nice_nano_v2-zmk.uf2` para o lado direito

## Troubleshooting

### Problemas de Conexão Bluetooth
1. Use o arquivo `settings_reset-nice_nano_v2-zmk.uf2`
2. Flashe novamente o firmware normal
3. Pareie novamente os dispositivos

### Problemas de Bateria
- Verifique se o RGB está configurado para desligar quando inativo
- Ajuste os tempos de idle e sleep no arquivo `corne.conf`

### Problemas de Sincronização
- Certifique-se de que ambos os lados estão com bateria
- Reset as configurações Bluetooth se necessário
- Verifique se está usando a mesma versão do firmware em ambos os lados

## Customização

Para personalizar sua configuração:
1. Modifique `corne.keymap` para alterar o layout
2. Ajuste `corne.conf` para configurações do sistema
3. Commit as alterações e deixe a Action compilar

## Contribuindo

Sinta-se livre para:
1. Abrir issues para reportar problemas
2. Enviar pull requests com melhorias
3. Compartilhar suas customizações

## Créditos

- ZMK Firmware: [zmkfirmware.dev](https://zmkfirmware.dev)
- Corne Keyboard: [foostan/crkbd](https://github.com/foostan/crkbd)
- Base config: [ZMK Config](https://github.com/zmkfirmware/zmk-config)

---

Made by [the spanish guy](https://github.com/the-spanish-guy) with :black_heart:

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
