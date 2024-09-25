# SHsotao_Banheiro

A aplicação `SHsotao_Banheiro` permite a automação de diversas funções da casa de banho, como iluminação, descarga, audio, aquecimento, fluxo e temperatura da agua do chuveiro e se integra com outras aplicações que automatizam outros cômodos.

## Recursos

- **EspNow**: Promova comunicação entre diferentes aplicações de automação dos cômodos sem a necessidade de uma rede wifi intermediária.

### Instalação

#### Dependências

Este projeto depende de algumas bibliotecas que devem ser instaladas manualmente. Siga os passos de acordo com o gerenciador que está utilizando:

##### Arduino IDE

1. Abra o Arduino IDE.
2. Vá para **Sketch** > **Include Library** > **Manage Libraries...**.
3. Na barra de pesquisa, digite `OneButton` e instale a biblioteca.
4. Para a biblioteca `SHtools_ESP32_OTA_AP`, será necessário instalá-la manualmente via Git. Siga os passos:
   - Vá para **Sketch** > **Include Library** > **Add .ZIP Library...**.
   - Baixe o ZIP da biblioteca diretamente do GitHub: [SHtools_ESP32_OTA_AP](https://github.com/ShafickCruz/SHtools_ESP32_OTA_AP).
   - Adicione o arquivo ZIP ao Arduino IDE usando a opção mencionada acima.

##### PlatformIO

Adicione as seguintes linhas ao seu `platformio.ini` para instalar automaticamente as dependências:

```ini
lib_deps =
    https://github.com/ShafickCruz/SHtools_ESP32_OTA_AP.git
    mathertel/OneButton@^2.6.1
```

#### Dependências

Certifique-se de que as seguintes bibliotecas estão instaladas em seu projeto:

```
#include <Arduino.h>
#include <WiFi.h>
#include <esp_now.h>
#include <SHtools_ESP32_OTA_AP.h>
#include <OneButton.h>
```

##### Informações Importantes

###### Inicialização do Serial

Este projeto **utiliza o monitor serial para depuração e comunicação**. Certifique-se de que a inicialização do Serial seja mantida no código principal, pois as bibliotecas, como `SHtools_ESP32_OTA_AP`, dependem dele para funcionar corretamente. O Serial deve ser inicializado no **setup()** com a taxa de baud correta, por exemplo:

```
void setup() {
    Serial.begin(115200);
    // Outros códigos de inicialização...
}
```

###### Dependências Externas

Certifique-se de que todas as bibliotecas dependentes estão instaladas corretamente. Veja a seção Instalação para mais detalhes.

###### Flags de Configuração

A biblioteca ElegantOTA utilizada em SHtools_ESP32_OTA_AP requer a definição de uma flag específica para ativar o modo assíncrono. As flags necessárias já estão definidas no platformio.ini da biblioteca. Caso experiencie erros relacionados, consulte a documentação de ElegantOTA ou tente adicionar a flag diretamente no arquivo platformio.ini:

```
build_flags = -DELEGANT_OTA_ASYNC
```

###### Comunicação ESP-NOW

Para que a comunicação via ESP-NOW funcione corretamente, é **necessário configurar o endereço MAC dos dispositivos ESP32 que se comunicarão com este projeto**. O MAC deve ser informado no código como um array de bytes em hexadecimal. Certifique-se de usar o endereço MAC correto do dispositivo peer para garantir o emparelhamento adequado.

Exemplo de configuração:

```
// Endereço MAC do ESP32 peer
static uint8_t PEER[]{0xxx, 0xxx, 0xxx, 0xxx, 0xxx, 0xxx};
```
