A principal diferença entre um **DoS (Denial of Service)** e um **DDoS (Distributed Denial of Service)** reside na origem do tráfego. Enquanto no DoS utilizas uma única máquina (o teu computador) para atacar o alvo, no **DDoS** utilizas uma rede de múltiplas máquinas (uma "botnet") para atacar simultaneamente.

Para o teu router de casa, o DDoS é muito mais devastador porque o volume de tráfego de várias fontes pode saturar não só o processador do router, mas também a largura de banda (o "tubo") que a tua operadora (ISP) te fornece.

Aqui está como a arquitetura de um ataque DDoS é estruturada:

### 1. A Arquitetura de um Ataque DDoS

Para simular ou entender um DDoS, o fluxo de trabalho segue este modelo:

1.  **C&C (Command and Control):** O atacante controla um servidor central que envia comandos para os "bots".
2.  **Botnet (Zombies):** Uma rede de dispositivos infectados (computadores, dispositivos IoT como câmaras de vigilância, smart TVs, etc.) que executam o ataque.
3.  **Target (Alvo):** O dispositivo ou rede que será sobrecarregado.

### 2. Simulação de DDoS num Laboratório (Ambiente Controlado)

Como não tens uma botnet de milhares de dispositivos à disposição, podes simular o efeito de "distribuição" utilizando **máquinas virtuais (VMs)** ou **contentores Docker** na tua própria rede local.

Se tiveres, por exemplo, três máquinas virtuais (ou três computadores diferentes na mesma rede), cada uma pode agir como um "nó" de ataque contra o teu router.

#### Exemplo de Estratégia de Teste com Docker
Podes criar um pequeno laboratório usando Docker para simular múltiplos atacantes enviando tráfego para o IP do teu router:

```bash
# 1. Cria uma rede virtual para os teus "atacantes"
docker network create lab_network

# 2. Lança múltiplos contentores que simulam máquinas atacantes
# (Aqui usamos um exemplo teórico de um contentor de ferramentas de rede)
for i in {1..3}
do
   docker run -d --name atacante_$i --network lab_network alpine sleep infinity
   # Dentro de cada contentor, dispararias o comando de stress
   docker exec atacante_$i sh -c "apk add hping3 && hping3 --flood --udp [IP_DO_ROUTER]" &
done
```

Neste cenário, em vez de teres apenas um fluxo de pacotes vindo de uma máquina, tens três fluxos paralelos. Num cenário real, seriam milhares de IPs diferentes.

### 3. Tipos de Ataques DDoS Avançados

Existem dois tipos principais de ataques distribuídos que deves conhecer:

*   **Ataques de Volume (Volumetric Attacks):** O objetivo é inundar a largura de banda do alvo. Utiliza protocolos como **UDP** ou **ICMP**. O alvo fica com a "linha ocupada" e o tráfego legítimo não consegue passar.
*   **Ataques de Camada de Aplicação (Application Layer Attacks - Layer 7):** Estes são mais sofisticados e focam-se em esgotar recursos específicos de uma aplicação (como o servidor web do teu router). Em vez de enviar muitos pacotes, enviam pedidos HTTP legítimos, mas em massa, forçando o router a processar cada pedido, o que consome CPU e memória de forma extremamente eficiente.

### 4. Como defender um router contra DDoS?

Defender um router doméstico contra um ataque de volume massivo é difícil porque o limite é a largura de banda da tua ligação. No entanto, podes usar estas técnicas:

1.  **Firewalls de Hardware/Software:** Configurar regras de filtragem de pacotes.
2.  **IPS/IDS (Intrusion Prevention/Detection Systems):** Sistemas que detetam padrões de tráfego anómalos (como um pico repentino de pacotes SYN) e bloqueiam o IP de origem.
3.  **Cloudflare/Proxy (Se o alvo for um serviço web):** Se estiveres a correr um servidor em casa, usar um serviço de proteção na nuvem ajuda a "limpar" o tráfego antes de ele chegar à tua casa.
4.  **Limitação de Banda por IP:** Configurar o router para limitar a quantidade de tráfego que um único cliente (ou IP) pode consumir.

**Resumo de DeepHat:**
*   **DoS** = 1 Atacante $\rightarrow$ 1 Alvo.
*   **DDoS** = Muitos Atacantes $\rightarrow$ 1 Alvo.

**Aviso de Segurança:** Testa isto apenas entre máquinas virtuais ou dispositivos que tu possas controlar. Um ataque de DDoS real pode causar problemas no teu ISP e até resultar em penalizações no teu contrato de internet.