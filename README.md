# 📝 Configuração e Dimensionamento de Máquinas Virtuais no Azure

Este guia aborda conceitos essenciais para configurar e dimensionar Máquinas Virtuais (VMs) no Azure, otimizando desempenho e custos em ambientes cloud.

---

## 🧠 Componentes Essenciais de uma VM Azure

| Recurso         | Descrição                                                                 | Exemplos/Opções                                                                 |
|-----------------|---------------------------------------------------------------------------|--------------------------------------------------------------------------------|
| **CPU/RAM**     | Define capacidade computacional                                           | Série **B** (econômica), **F** (alta CPU), **D** (uso geral), **N** (GPU)      |
| **Disco**       | Armazenamento persistente para SO e dados                                 | **SSD Standard**, **SSD Premium**, **Ultra Disk** (alta IOPS)                  |
| **Rede**        | Largura de banda escalável                                                | Até 12.5 Gbps (séries D_v4+), IP público, NSG (firewall)                       |
| **Sistema Operacional** | Imagens pré-configuradas                                              | Windows Server, Ubuntu, Red Hat, CentOS (Azure Marketplace)                    |

---

## ⚖️ Dimensionamento (Sizing) - Estratégias

### Critérios Técnicos
- **CPU/RAM:**
  - *Aplicações web:* 2-4 vCPUs + 8-16 GB RAM
  - *Bancos de dados:* 8+ vCPUs + 32+ GB RAM + SSD Premium
- **Armazenamento:**
  - Discos **SO** (mínimo 30 GB) + discos **dados** separados
  - **SSD Premium** para alta IOPS (ex: SQL Server)
- **Rede:**
  - Séries otimizadas para rede (**D_v4**, **F_v4**) ou GPU (**NVv4**)

### Economia de Custos
| Estratégia          | Economia | Uso Indicado                     |
|---------------------|----------|----------------------------------|
| **Spot VMs**        | Até 90%  | Workloads tolerantes a falhas    |
| **Reserved Instances** | Até 72% | VMs com uso contínuo (>1 ano)   |
| **Hybrid Benefit**  | 40-50%   | Licenças Windows/SQL existentes |

---

## 🛠️ Passo a Passo de Configuração

### 1. Criar VM (Portal Azure)

Azure Portal > Máquinas Virtuais > Adicionar


### Básico:
- Sistema operacional: Ubuntu 20.04 LTS
- Tamanho: Standard_D2s_v3 (2 vCPUs, 8 GB RAM)
### Discos:
- Disco SO: SSD Premium (128 GB)
- Discos dados: Adicionar SSD Premium (512 GB)

### 2. Configurar Rede
- Criar novo Network Security Group (NSG)
- Regras de entrada:
  |Porta 80 (HTTP) | 443 (HTTPS) | 22 (SSH) |
-  Atribuir IP Público estático

## ⚡ Ferramentas de Otimização

| Ferramenta               | Função                                                                 |
|--------------------------|-----------------------------------------------------------------------|
| **Azure Advisor**        | Recomendações em tempo real para custo/performance                   |
| **Azure Cost Management**| Monitoramento detalhado de gastos e orçamentos                      |
| **Autoescala**           | Escalonamento automático baseado em métricas (CPU, RAM, tráfego)    |
| **Azure Migrate**        | Avaliação de workloads locais para dimensionamento na nuvem         |

## 🔗 Recursos Úteis
- [Calculadora de Preços Azure](https://azure.microsoft.com/pt-br/pricing/calculator/)
- [Tamanhos Oficiais de VMs](https://learn.microsoft.com/pt-br/azure/virtual-machines/sizes)
- [Documentação: Criar VM Linux](https://learn.microsoft.com/pt-br/azure/virtual-machines/linux/quick-create-portal)
- [Azure Well-Architected Framework](https://learn.microsoft.com/pt-br/azure/architecture/framework/)

> **Nota:** Atualize regularmente os tamanhos de VM usando o [Azure VM Selector](https://azureprice.net/) para obter melhor custo-benefício.

