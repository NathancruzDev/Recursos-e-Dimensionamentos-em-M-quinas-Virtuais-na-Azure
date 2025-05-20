# Fundamentos de Computação e Redes no Microsoft Azure

O Azure oferece uma base flexível e escalável para execução de aplicativos, desde máquinas virtuais tradicionais até soluções modernas baseadas em contêineres e computação sem servidor.

---

## 1. Computação no Azure

### Máquinas Virtuais (Azure Virtual Machines)

As máquinas virtuais permitem criar e executar VMs com sistemas Windows ou Linux, configuradas conforme a necessidade do projeto. Elas são utilizadas para hospedar aplicações, bancos de dados ou serviços que exigem controle total do sistema operacional.

- Ao criar uma VM, o Azure provisiona armazenamento, rede e processamento de forma isolada, mas integrada ao ecossistema da nuvem.

### Alta Disponibilidade com Conjuntos de Disponibilidade

Para garantir que os serviços continuem funcionando mesmo diante de problemas com hardware, as VMs podem ser distribuídas em Conjuntos de Disponibilidade, que utilizam:

- Domínios de Falha (Fault Domains): garantem que VMs estejam em racks físicos diferentes.
- Domínios de Atualização (Update Domains): permitem atualizações sem afetar todas as VMs ao mesmo tempo.

Assim, mesmo que um rack apresente falha, outra instância ativa em outro domínio garante a continuidade dos serviços, evitando quedas ou interrupções

### Escalabilidade com Conjuntos de Escala

O Virtual Machine Scale Set (VMSS) permite instânciar conjuntos de VMs idênticas, que escalam automaticamente com base na demanda (por exemplo, mais usuários acessando um site). Isso garante desempenho consistente e economia de recursos.
Ideal 80/20 para 2 e 40/60 para -1;

---

## 2. Contêineres e Computação Serverless

Além das VMs, o Azure oferece outras opções mais leves e ágeis para executar aplicações.

### Instâncias de Contêiner

Com o Azure Container Instances (ACI), é possível rodar contêineres de forma isolada, sem precisar configurar uma VM. Tem boa utilidade para cargas de trabalho rápidas e temporárias.

### Azure Kubernetes Service (AKS)

Para aplicações mais complexas em contêineres, o AKS fornece uma plataforma completa de orquestração baseada em Kubernetes. Ele automatiza o balanceamento, escalonamento e atualizações, sendo ideal para arquiteturas de microsserviços(sempre que ler microsserviços lembrar das aulas iniciais de Java).

### Azure Functions

O Azure Functions é o serviço de computação serverless do Azure. Permite executar código em resposta a eventos (como requisições HTTP, filas e timers) sem necessidade de gerenciar servidores. Você paga apenas pelo tempo de execução.

---

## 3. Rede no Azure: Comunicação e Segurança

Os serviços de computação se conectam por meio da infraestrutura de rede do Azure, projetada para oferecer segurança, desempenho e integração com redes locais.

### Rede Virtual (VNet)

Toda VM, contêiner ou função é implantada dentro de uma Virtual Network (VNet), que age como uma rede privada na nuvem. Dentro dela, é possível criar:

- Sub-redes para separar funcionalidades (ex.: front-end, banco de dados);
- NSGs (Network Security Groups) para controlar o tráfego de entrada/saída por IP, porta e protocolo.

### Gateway VPN e ExpressRoute

Para integrar com redes locais (on-premises), o Azure oferece:

- VPN Gateway: cria túneis seguros sobre a internet (IPsec/IKE).
- ExpressRoute: conexão dedicada e privada entre seu datacenter e o Azure (sem passar pela internet), com latência mais baixa e maior confiabilidade.

### Load Balancer e Application Gateway

- Azure Load Balancer: distribui o tráfego entre várias VMs em uma mesma camada de rede (camada 4 - TCP/UDP).
- Application Gateway: oferece balanceamento com inspeção de aplicação (camada 7 - HTTP), além de WAF (Web Application Firewall) para proteção de aplicativos web.

---

## 4. Arquitetura Prática e Interconexão de Serviços

Um sistema real geralmente combina vários desses serviços. Exemplo:

1. Máquinas Virtuais são criadas dentro de uma VNet, com escalabilidade via VM Scale Set.
2. Um Load Balancer distribui o tráfego entre as instâncias, garantindo alta disponibilidade.
3. O Application Gateway protege os aplicativos com WAF e realiza roteamento inteligente.
4. A comunicação com o ambiente local é feita por VPN Gateway ou ExpressRoute.
5. Aplicações auxiliares são executadas via Azure Functions ou Instâncias de Contêineres, otimizando recursos.
6. A segurança e segmentação da rede são garantidas com NSGs, sub-redes e conjuntos de disponibilidade.

> 💡 Atenção: monitore recursos órfãos, como discos não utilizados, que continuam gerando custo mesmo sem estarem associados a uma VM.

---

