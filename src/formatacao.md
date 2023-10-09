- [Informações para Formatação e construção de HD Bootavel](#informações-para-formatação-e-construção-de-hd-bootavel)
  - [Ventoy](#ventoy)
    - [Formatação particionada](#formatação-particionada)
    - [Instalação no linux](#instalação-no-linux)
- [Notebook positivo motion q4128c](#notebook-positivo-motion-q4128c)
- [Informações adquiridas a respeito de formatação](#informações-adquiridas-a-respeito-de-formatação)
  - [Tecnologias de formatação](#tecnologias-de-formatação)












## Informações para Formatação e construção de HD Bootavel

### Ventoy
 - Aplicativo focado na construção de pendrive/HD bootavel. 
 - Tem capacidade de inserir várias ISOs no mesmo pendrive/HD
 - [Ventoy Download](https://www.ventoy.net/en/download.html)

#### Formatação particionada

O aplicativo Exige que todo HD seja formatado e ele não será mais particionável

#### Instalação no linux

1. Baixe o arquivo zipado e extraia
2. Execute o arquivo `Ventoy2Disk.sh` como root com o seguinte comando:
3. `sudo sh Ventoy2Disk.sh -i /dev/sdX` onde X é a letra do seu HD
4. Verifique que o HD foi criado e renomeado para Ventoy e que ele tem 2 partições
5. Monte a partição com nome de Ventoy e copie as ISOs para dentro dela
   
---

## Notebook positivo motion q4128c
[Link com Informações a respeito de formatação do notebook](https://www.meupositivo.com.br/para-voce/suporte-tecnico/drivers)

---

## Informações adquiridas a respeito de formatação

### Tecnologias de formatação


 - MBR
   - Limite de 2TB
   - 4 partições primárias
 - GPT
   - Virtualmente Sem limite
   - 128 partições primárias
   - 18 exabytes
   - 