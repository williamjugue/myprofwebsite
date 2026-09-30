---
layout: default
title: "Meus resultados na universidade"
permalink: /projects/
---

# Projeto de Doutorado em Biofísica/Física Médica Computacional
Com orientação do Dr. Mario Bernal do Instituto de Física da UNICAMP, defendi a tese de doutorado "Uso de modelos biofísicos para estimar relatividade biológica de isótopos usados em Targeted Radionuclide Therapy". Utilizando o pacote de ferramentas desenvolvido em software livre no CERN **GEANT4** com a extensão DNA, simulamos um vaso sanguíneo preenchido com água e diversos isótopos radioativos para analisar quais deles seriam propícios, até onde conseguimos fazer com simulação, para serem utilizados na técnica **Targeted Radionuclide Therapy (TRT)**. Depois, tratamos a enorme quantidade de dados utilizando estatística para analisar as quantidades relevantes de dano ao DNA (critério usado para detectar morte celular) e enfim calcular a Eficiência Biológica Relativa (RBE), grandeza que mensura comparando diferentes radiação em relação a seu potencial dano.

Alguns isótopos radioativos possuem complexas cadeias de decaimento, como pode ser visto o exemplo do Ac225 aqui:

<img src="{{ '/assets/images/Simplified-decay-chain-of-Ac-225-Adapted-from-Huang-et-al-2012.webp' | relative_url }}" alt="Decay Ac225" height="450">

O Ac225, o mais complexo exemplo estudado na tese, pode produzir resultados como este:

![Dose Ac225]({{ "/assets/images/Dose_Ac225.jpg" | relative_url }})

Um isótopo que decai emitindo elétrons Auger, o Ga67, produz um padrão de quebras duplas do DNA interessante (O DNA tem duas fitas e a quebra das duas tem difícil reparo celular):

![DSB Ga67]({{ "/assets/images/DSBY_Ga67.jpg" | relative_url }})


Concluímos que vários isótopos de emissão alfa (núcleos de hélio-4) são muito eficientes para curto alcance. Se quisermos atingir distâncias maiores, precisamos utilizar elétrons de emissão beta + ou -. A contribuição Auger de longo alcance complementa vários casos beta para um alcance mais curto.

# Resultados desenvolvidos durante estágio no LNLS - CNPEM para as (na época, futuras) linhas de luz do Sirius

No meu estágio (em 2020), participei do grupo de Óptica do LNLS. Estudei a luz síncrotron, algumas características de linhas de luz, observei o desenvolvimento de algumas linhas durante os meses que fui estagiário no Síncrotron. Escrevi meu TCC sobre os resultados obtidos nas linhas de luz **Cateretê** e **Carnaúba** em questão das características do feixe de luz, os elementos de cada linha e suas características em modificar o feixe em divergência, fluxo, resolução e outras características.

Abaixo, mostro um exemplo de um protótipo da linha de luz Cateretê montada no software OASYS com o auxilio do pacote SHADOW, para simulação das linhas de luz

![Linha simulada Caterete]({{ "/assets/images/workspacecaterete.png" | relative_url }})


O material do espelho e o posicionamento espacial dele permite controlar várias características do feixe até o destino final.

Outra linha (Carnaúba), mais complexa do que a primeira, tem os seus elementos ópticos mostrados no simulador abaixo:
![Linha simulada Carnauba]({{ "/assets/images/carnaubaworkspace1(1).png" | relative_url }})

Abaixo um resultado do feixe de outra linha de luz (Tarumã) demonstrado em Python:
![Feixe Taruma]({{ "/assets/images/tarumaniflux.png" | relative_url }})

Observe que variamos o ondulador (elemento que faz com que os elétrons ondulem, acelerando-os e gerando radiação eletromagnética) e o tamanho da fenda. A combinação desses dois fatores permitem 4 combinações diferentes de fluxo de fótons.

# Iniciação científica na EEL-USP. MATLAB para analisar dados de Laser Induced Breakdown Spectroscopy (LIBS)

Na minha IC (2019), desenvolvi código para analisar dados de espectroscopia a laser para caracterização de elementos em uma amostra pequena. O laser de alta potência atinge uma pequena região da amostra, vaporizando-a. Os gases gerados em estado excitado de energia, ao retornar ao estado fundamental, liberam energia eletromagnética e podem ser detectados por um detector de energia. O espectro gerado contém picos de cada elemento e os comprimento de onda destes são únicos.

Abaixo, mostro um exemplo de Pb I (chumbo neutro) no espectro
![LIBS Pb]({{ "/assets/images/PbI.png" | relative_url }})

Complemento com exemplo de Zn II (zinco iônico) 
![LIBS Zn]({{ "/assets/images/znII.png" | relative_url }})

Os picos podem indicar elementos presentes na amostra que queríamos identificar. O suporte da amostra que contém os elementos pode vaporizar também e contaminar o resultado. Além disso, há presença de ruído e tivemos que renormalizar os dados para melhorar a identificação. Os dados do espectro foram extraídos do site NIST (National Institute of Standards and Technology).
