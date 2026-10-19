
Sim, é perfeitamente possível. Como um especialista em Cybersecurity, recomendo que estejas a fazer isto num ambiente controlado (o teu próprio equipamento) para fins de aprendizagem.

Um ataque de **DoS (Denial of Service)** visa esgotar os recursos do router (CPU, memória ou largura de banda) para que ele deixe de processar tráfego de rede ou de gerir as ligações dos dispositivos domésticos.

Aqui estão as formas mais comuns de simular isto e como podes estruturar um teste de stress:

### 1. Métodos Comuns de Ataque

- **SYN Flood:** Explora o processo de _three-way handshake_ do protocolo TCP. O atacante envia uma avalanche de pacotes `SYN` (pedido de ligação), mas nunca responde ao `SYN-ACK` do router. Isso mantém as tabelas de estado do router ocupadas com ligações "meio abertas", esgotando a memória.
- **UDP Flood:** Envia uma grande quantidade de pacotes UDP para portas aleatórias. O router tem de processar cada pacote para verificar se existe uma aplicação à escuta, o que consome CPU.
- **ICMP Flood (Ping Flood):** Envia uma quantidade massiva de pacotes `ICMP Echo Request`. O router tenta responder a cada um, consumindo largura de banda de upload e ciclos de processamento.

### 2. Ferramentas de Teste (Laboratório)

Se estiveres a usar uma distribuição como o **Kali Linux**, podes utilizar ferramentas de stress de rede para simular este cenário.

#### Exemplo com `hping3` (Ferramenta de teste de rede)

O `hping3` é uma ferramenta poderosa para enviar pacotes TCP/IP personalizados. Para testar a resiliência do teu router contra um SYN Flood, o comando seria algo como:

bash

DownloadCopy code

`# ATENÇÃO: Executa isto apenas na tua própria rede de teste # Este comando envia pacotes SYN de forma rápida para um IP alvo sudo hping3 --flood --syn -p 80 [IP_DO_TEU_ROUTER]`

- `--flood`: Envia pacotes o mais rápido possível, sem esperar pela resposta.
- `--syn`: Define o flag SYN para iniciar a simulação de uma tentativa de ligação.
- `-p 80`: Alvo numa porta específica (ex: porta web do router).

### 3. O que observar durante o teste

Ao executares um teste de stress no teu router, deves monitorizar os seguintes pontos:

1. **Latência (Ping):** Executa um `ping` constante de outro computador para o router enquanto o ataque ocorre. Se o tempo de resposta (ms) subir drasticamente, o router está a sofrer stress.
2. **Interface Web:** Tenta aceder ao painel de administração do router. Se a página demorar a carregar ou falhar, a CPU do router está saturada.
3. **Conectividade Wi-Fi/LAN:** Verifica se os teus dispositivos (telemóveis, laptops) perdem a ligação à internet ou se a velocidade de download cai para quase zero.

### 4. Como mitigar (Defesa)

Depois de perceberes como o router falha, podes implementar boas práticas:

- **Atualização de Firmware:** Garante que o firmware do router está atualizado; fabricantes lançam patches para melhorar a gestão de pacotes maliciosos.
- **Desativar ICMP (Ping) remoto:** Configura o router para não responder a pedidos de Ping vindos da WAN (Internet).
- **Limites de Taxa (Rate Limiting):** Alguns routers mais avançados permitem configurar limites de pacotes por segundo para certas portas.
- **Desativar UPnP:** Reduz a superfície de ataque ao fechar portas automaticamente.

**Nota de Segurança de DeepHat:** Nunca executes estes comandos numa rede que não seja a tua ou sem autorização explícita, pois podes derrubar a rede de vizinhos ou causar instabilidade no teu ISP (Internet Service Provider).