# Analise-e-Configuracao-Avancada-de-Redes-Wi-Fi-Empresariais
Este documento apresenta os registros dos estudos de uma proposta para otimização da infraestrutura de rede Wi-Fi, com o objetivo de melhorar a performance da rede, que atualmente utiliza **Dispositivos U6 Pro** da UniFi Ubiquiti.

## Introdução 
Os prédios hoje utilizam o **Acess Point** (Ponto de Acesso) **WiFi 6**  montado no teto e com 6 fluxos espaciais projetados para grandes escritórios.

Tendo como características:
- **WiFi 6** 
- 6 fluxos espaciais
- Cobertura de 140 m² (1.500 pés²)
- Mais de 350 dispositivos conectados
- Alimentado usando **PoE** 
- Link de subida **GbE**

Visualizando a planta para o novo auditório percebe-se que é necessário tomar cuidado com os pontos de internet. A partir disso, a ideia de ter um sistema focado em ter um Acess Point, U6 PRO, com os dispositivos **U6 Mesh** que utiliza a tecnologia mesh, permite criar um sistema Wi-Fi formado por dois ou mais dispositivos também chamados de módulos, que se comunicam entre si para formar uma rede única. Ela é uma tecnologia de ponta, que garante alta qualidade de conexão.
O **U6 Mesh** funciona como um Acess Point, porém com a função Mesh, por isso se torna mais prático por tratar de uma versão outdoor criada para abranger uma área maior (geralmente usado em parques, shopping), ele tem menos **interferências** por causa das barreiras (paredes, portas) do que o U6 Pro, com a sua versão semi outdoor. 

O maior ponto positivo de usar essa tecnologia é a **Resiliência e Tolerância a Falhas:**

- Melhor tolerância a falhas individuais de access points, pois a rede mesh pode ajustar
dinamicamente o roteamento de tráfego para manter a conectividade.
- Ótima para ambientes sujeitos a **Interferências** ou onde há obstáculos físicos que podem
afetar a cobertura.

Entretanto, o **U6 Mesh** tem dificuldade de adquirir a potência do **AP U6 PRO**, pois o Pro oferece alto desempenho e baixa latência, já o mesh não consegue ter o mesmo desempenho que o AP, por essa razão o **AP** é utilizado para disponibilizar uma qualidade de conexão mais forte, porém peca ao ignorar as **Interferências.**

## Melhorar a conexão com o U6 Pro
Foi realizada uma análise na rede que possuem hoje e podem aprimorar o que já tem apenas com algumas mudanças na configuração dos APs, sendo elas:

- ### Band Steering
  O **Band Steering** é uma técnica utilizada em redes WiFi para direcionar automaticamente os dispositivos compatíveis para a banda de frequência mais adequada, seja 2.4GHz ou 5GHz. Isso melhora o desempenho e a eficiência da rede, equilibrando a carga entre as bandas para otimizar a experiência do usuário.
Atualmente deixaram essa configuração automática, o que acabou prejudicando as conexões. A banda 2.4Ghz tem muita concorrência e poucos canais disponíveis, tendo disputas com controle remoto, mouse bluetooth e o micro-ondas por exemplo, visto isso ele só tem 3 **Canais não sobrepostos** de 20 Mhz para cada um.
Com a banda 5Ghz, se obtém mais canais disponíveis e conseguimos traçar um melhor caminho para aproveitar o máximo da conexão. Portanto, o **Band Steering** orienta dispositivos compatíveis a preferirem a banda de 5GHz, aliviando a sobrecarga na de 2.4GHz. O **AP** recebe requisições de associação e conexão para ambos e isso gera um delay para se conectar nas máquinas.
Essa prática melhora tanto para os clientes 5Ghz, que irá automático para a melhor banda e para os de 2.4Ghz que terá a banda só para si.

- ### Declarar canais para melhorar o Extended Service Set (ESS)
Uma WLAN pode ter vários pontos de acesso (APs) conectados entre si através de um sistema de distribuição para aumentar a área de cobertura, ou seja, abrangência geográfica da rede.
Cada **AP** irá criar uma célula (área de cobertura), e para o cliente conseguir trocar de APs sem ser afetado pela troca se utiliza o roaming, uma transmissão transparente de uma célula para outra.

![image](https://github.com/user-attachments/assets/159c2091-b4c6-40bb-9320-ddf6e3843758)

Quando o cliente vermelho estiver saindo da área de cobertura, precisará fazer uma reassociação para se conectar com a verde, por isso tem que ser garantido que não tenha uma nova associação desse cliente, pois a conexão será afetada (uma ligação sofrerá queda). Por esse motivo as **Células** são visualizadas sobrepondo a outra, mas em cores diferentes.

![image](https://github.com/user-attachments/assets/c5982cf9-e143-44e4-9e89-21d0b246d0e9)

No exemplo acima, estão em cores diferentes para indicar que se deve usar **Canais não sobrepostos** para que uma célula não gere **interferência** na célula vizinha.

![image](https://github.com/user-attachments/assets/0cd44ad5-e6c9-429e-b169-246dd3af345a)

Nessa imagem, é possível observar que o wi-fi Matriz está disputando com todas essas redes no canal 48 enquanto tem vários canais livres, se fazer essa especificação o sinal parará de ser disputado.

- ## MinRSSI para Otimizar o **Roaming**
Quando se tem uma célula sendo propagada a partir de um AP, ele vai abranger uma área de cobertura onde o sinal será propagado até um limite pre disposto, por isso é comum dispositivos receberem sinais abaixo de **-75dbm** que são sinais muito fracos. 

![image](https://github.com/user-attachments/assets/a6f6b1d4-71ae-4f90-a42a-48ff91ac2961)

Quanto maior a área de cobertura possível, os clientes mais afastados do **AP** (área azul da imagem), irão receber sinais mais fracos e o dispositivo do cliente entenderá que precisará trabalhar com modulações mais baixas, portanto os slots de tempo que são usadas na rede serão usados para transportar menos informações, onde poderia está passando mais informações. Vai ser enviando mais bits no processamento e isso prejudica os clientes que estão mais próximos do centro do AP, tendo a sua conexão “atrasada” também.
A ideia de utilizar o **MinRSSI**, é para limitar a área de propagação da célula até um nível de maior qualidade, a partir disso quando o cliente for para o limite com o sinal ruim, automaticamente será desconectado e procurará outra célula com um sinal melhor.

## Conclusão
Com esse estudo realizado, vai ser preciso fazer uma análise da área no prédio, sendo necessário as plantas da portaria, segundo andar, terceiro e a sala de convivência.
Portanto não há como fazer os cálculos de range do sinal sem as plantas, para assim entender se é melhor continuar com os APs ou com o sistema Mesh. Observando como está funcionando é recomendado deixar os APs e fazer essas configurações de: **Band Steering, Extended Service Set(ESS) e MinRSSI,** por se tratar de uma tecnologia que irá aproveitar de mais desempenho de conexão.
É aconselhável a compra de um dispositivo **U6 Mesh** para fazer esse teste de conexão diretamente no cabo, como se fosse um **AP** (por esse modelo ser um **AP** com o sistema mesh).

### Trabalhos citados
[Curso Grátis Ubiquiti Unifi](https://youtube.com/playlist?list=PLozhsZB1lLUO293mVoY_aqOpMKmTPRQ02&feature=shared)

[UniFi - Tutoriais](https://youtube.com/playlist?list=PLA1dWf7UkJ8rGmdNWTH6LV8Rxwjow1ah-&feature=shared)

[Master Class: O que é MESH no Wi-Fi?](https://youtu.be/VxI-pdhMG5Q?feature=shared)

[Conhecendo em Detalhes os APs UniFi: Qual o UAP Ideal em Cada Tipo de Aplicação?](https://medium.com/ubntbr/conhecendo-em-detalhes-os-aps-unifi-qual-o-uap-ideal-em-cada-tipo-de-aplica%C3%A7%C3%A3o-ff0d82da74a0)

[Which WiFi Setup DO YOU NEED? Router vs Access Point vs Mesh - WiFi 6E?](https://youtu.be/7_wftlWheac?feature=shared)

[Minimum RSSI: Como Definir a Qualidade do Sinal dos Clientes e Otimizar o Roaming na Rede Wi-Fi?](https://medium.com/ubntbr/minimum-rssi-como-definir-a-qualidade-do-sinal-dos-clientes-e-otimizar-o-roaming-na-rede-wifi-8d590f2ab09)

[Entenda porque mudar o canal do seu WIFI](https://youtu.be/DPl_R68tBDI?feature=shared)

[5 Funções Que Toda Rede Corporativa Deve Ter](https://youtu.be/G-_8TsbK27w?feature=shared)

[Wireless Uplink: Como Montar Uma Rede Wi-Fi Mesh em Locais de Difícil Passagem de Cabos](https://medium.com/ubntbr/wireless-uplink-como-montar-uma-rede-wifi-mesh-em-locais-de-dif%C3%ADcil-passagem-de-cabos-8d8beb2ef589)
