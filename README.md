# Orçamentos técnicos | Calman Caldeiraria

Site estático, em um único arquivo `index.html`, que transforma o esboço enviado pelo cliente em um orçamento técnico de caldeiraria completo e editável. A inteligência artificial (Claude, da Anthropic) elabora a primeira versão com o método de um supervisor sênior de orçamentos; a equipe revisa, ajusta e aprova antes de enviar a proposta.

> **Revisão humana obrigatória.** Os valores gerados são estimativas de referência. Quantidades, preços, premissas e exclusões devem ser conferidos por quem assina a proposta. A ferramenta não substitui projeto estrutural, memorial de cálculo, ART nem a responsabilidade técnica da empresa.

## O que a ferramenta entrega

Para cada solicitação, o site monta o escopo por etapa (detalhamento, suprimento, fabricação, tratamento superficial, transporte, montagem e entrega) e a lista de insumos com memória de cálculo, perdas, preço nacional, regional e adotado e grau de confiança. A mão de obra aparece separada por função e por local (oficina e campo), com profissionais, dias, horas e HH. Completam o orçamento os equipamentos, os serviços de terceiros e os custos indiretos da obra, inclusive os de SST (integração, EPI, exames e treinamentos).

A aba Mercado compara os preços adotados com as médias nacional e regional e mostra a curva ABC. A aba Pontos a avaliar reúne o que o esboço não prevê e pode mudar custo, prazo ou segurança: sobrecarga, normas de projeto, ensaios, pintura, içamento, NR 10, NR 12, NR 33, NR 35, retenções tributárias e outros. Cada ponto tem custo potencial, e as perguntas ao cliente saem prontas para copiar. A aba Viabilidade dá o veredito, o preço mínimo sem lucro e a ocupação da equipe.

Também é possível trabalhar sem IA. Todas as tabelas aceitam inserção manual, há modelos por tipologia e um estimador paramétrico de insumos e mão de obra a partir do peso de aço. A composição do custo do HH considera insalubridade (NR 15) e periculosidade (NR 16), sem acumular os adicionais.

As saídas são a proposta técnico-comercial para o cliente ou o relatório interno completo, impressos em PDF pelo navegador, e uma planilha Excel com fórmulas ligadas entre as abas. O site traz ainda um exemplo preenchido e a aba Guia de uso, com a explicação de cada tela.

## Arquivos do repositório

O `index.html` é o site completo, com HTML, CSS e JavaScript no mesmo arquivo. O `README.md` é este guia. Opcionalmente, coloque um `logo.png` com o logotipo da empresa na raiz do repositório, ao lado do `index.html`: o site o usa no menu e no cabeçalho da proposta.

## Publicar no GitHub Pages

1. Crie uma conta em github.com ou use a conta da empresa.
2. Clique em **New repository**, dê um nome (por exemplo, `orcamentos-calman`), marque **Public** e clique em **Create repository**.
3. Na página do repositório, clique em **Add file** e depois em **Upload files**. Arraste o `index.html`, este `README.md` e, se quiser, o `logo.png`. Clique em **Commit changes**.
4. Abra **Settings** e depois **Pages**. Em **Build and deployment**, escolha **Deploy from a branch**, selecione a branch `main` e a pasta `/ (root)` e clique em **Save**.
5. Aguarde de 1 a 3 minutos e recarregue a página. O endereço aparece no topo da seção Pages, no formato `https://SEU-USUARIO.github.io/orcamentos-calman/`.

Para atualizar o site, envie um novo `index.html` pelo mesmo caminho. O GitHub substitui o arquivo e republica em poucos minutos. Orçamentos e configurações não são afetados, porque ficam no navegador de cada usuário.

No plano gratuito, o GitHub Pages exige repositório público, e o site fica acessível a quem tiver o endereço. Isso não expõe orçamentos nem a chave da API, que ficam somente no navegador de quem usa. Mesmo assim, não grave preços internos nem dados de clientes diretamente no código.

Para testar antes de publicar, abra o `index.html` com dois cliques no Chrome ou no Edge. O modo manual e o exemplo funcionam dessa forma. Se a chamada à IA for bloqueada pelo navegador, use o endereço do GitHub Pages, que funciona por https.

## Configurar a inteligência artificial

1. Acesse platform.claude.com e crie a conta da organização.
2. Adicione créditos. A API é cobrada por uso e é separada das assinaturas do Claude.ai.
3. Defina um limite de gastos mensal para a organização. É a principal proteção caso a chave seja usada indevidamente.
4. Em **API keys**, crie uma chave com nome identificável (por exemplo, `site-orcamentos`) e copie o valor, que começa com `sk-ant-`.
5. No site, abra **Configurações**, cole a chave e clique em **Testar conexão**. A mensagem informa quantos modelos a chave acessa e se o modelo escolhido está disponível.
6. Opcional: marque **Pesquisar preços atuais na internet**. A busca web precisa estar habilitada pelo administrador da organização no Console; sem isso, a geração retorna erro e o site explica como resolver.

O modelo padrão é o Claude Sonnet 5, com bom equilíbrio entre qualidade, velocidade e custo. O Claude Opus 5.5 é indicado para esboços complexos ou com muitas folhas; o Claude Fable 5.1 tem a maior capacidade e o maior custo; o Claude Haiku 4.5 atende pedidos simples com menor custo. O limite de saída padrão é de 64.000 tokens e pode ser elevado até 128.000 (no Haiku 4.5, o máximo é 64.000).

## Custos aproximados

**Tabela 1 - Custo estimado da API por orçamento gerado**

| Modelo | Entrada (US$ por milhão de tokens) | Saída (US$ por milhão de tokens) | Custo por orçamento (US$) |
|:--|--:|--:|--:|
| Claude Haiku 4.5 | 1,00 | 5,00 | 0,10 a 0,30 |
| Claude Sonnet 5 (padrão) | 2,00 | 10,00 | 0,20 a 0,60 |
| Claude Opus 5.5 | 4,00 | 20,00 | 0,45 a 1,20 |
| Claude Fable 5.1 | 10,00 | 50,00 | 1,15 a 2,90 |

Fonte: tabela de preços da Anthropic (platform.claude.com/docs/en/about-claude/pricing), consulta em setembro de 2026; custo por orçamento estimado com base no consumo típico da ferramenta.
Nota: considera de 15 a 40 mil tokens de entrada (instruções, base de preços e esboço) e de 20 a 50 mil tokens de saída (raciocínio e orçamento estruturado). A pesquisa na internet custa US$ 10 por mil buscas (US$ 0,01 cada), além dos tokens do conteúdo encontrado; com 5 buscas, acrescente cerca de US$ 0,10 a 0,40. A revisão crítica custa, em geral, menos de US$ 0,10 com o Sonnet 5. Os preços podem ser alterados pela Anthropic; acompanhe o consumo real no Console.

## Fluxo recomendado

1. **Novo orçamento.** Preencha cliente, obra, município e tudo o que não está no esboço (altura, prazo, condições de acesso, exigências do cliente).
2. **Esboço.** Anexe fotos, PDF, planilha ou Word. Uma imagem copiada pode ser colada com Ctrl+V. Arquivos CAD (DWG, DXF) precisam ser exportados em PDF.
3. **Geração.** Clique em Gerar orçamento com IA (de 1 a 4 minutos) ou monte manualmente a partir do modelo da tipologia e do estimador.
4. **Revisão das tabelas.** Siga a ordem Escopo (premissas e exclusões), Insumos (memória de cálculo e itens de confiança baixa), Mão de obra (HH por tonelada coerente com o histórico da empresa), Equipamentos e terceiros, Indiretos e BDI.
5. **Mercado.** Confira os alertas de desvio acima de 25% e faça cotação formal dos itens classe A da curva ABC.
6. **Pontos a avaliar.** Marque cada ponto como verificado ou não se aplica, inclua no custo o que for necessário e envie as perguntas ao cliente pelo botão de copiar.
7. **Viabilidade.** Só avance com veredito favorável ou com as ressalvas registradas nas premissas e exclusões. Peça a revisão crítica pela IA como segunda opinião.
8. **Proposta.** Marque Aprovado internamente (a marca d'água Minuta sai do documento), escolha o modo cliente e imprima em PDF. Salve o arquivo `.json` do orçamento junto com a proposta enviada.

## Dados, privacidade e segurança

**Onde ficam os dados.** Orçamentos, histórico (até 30 versões), base de preços, configurações e a chave da API ficam no armazenamento local do navegador, no computador de quem usa. Nada é gravado no GitHub. Outro computador ou outro navegador começa vazio: para levar os dados, use Exportar e Importar cópia de segurança, em Configurações, ou salve cada orçamento em `.json`. Limpar os dados de navegação apaga tudo, por isso faça cópias de segurança com frequência.

**Arquivos dos clientes.** O esboço e as informações do pedido são enviados diretamente do navegador para a API da Anthropic, somente no momento da geração. Os anexos não ficam salvos no site. Antes de usar a ferramenta com clientes que exigem sigilo, confirme se os acordos de confidencialidade permitem o processamento por serviços de terceiros.

**Chave da API.** A chave fica gravada no navegador em que foi colada, e qualquer pessoa com acesso a esse navegador pode usá-la. Use o site em computadores da empresa. Em máquinas compartilhadas, clique em Apagar chave ao terminar. Mantenha o limite de gastos no Console e, se suspeitar de vazamento, revogue a chave e crie outra. A cópia de segurança exportada não inclui a chave.

## Base de preços e parâmetros

A base inicial tem cerca de 85 itens. Os que indicam código SINAPI usam os preços de maio de 2026 (média nacional, não desonerado); os demais são estimativas editáveis. O fator regional padrão de mão de obra e serviços para Minas Gerais é 0,94, obtido pela razão entre o custo médio do metro quadrado do SINAPI em MG (R$ 1.857,18) e no Brasil (R$ 1.976,37) em junho de 2026. O fator de materiais começa em 1,00.

O salário mínimo de R$ 1.621,00 (Decreto 12.797/2025) é a base de cálculo da insalubridade. Os encargos sociais padrão são de 114% (horista, não desonerado) e devem ser confirmados com a contabilidade.

O BDI padrão é de 30,18%, composto por administração central 5%, seguros 0,8%, riscos 1,5%, garantias 0,5%, despesas financeiras 1%, lucro 10% e tributos 8%, calculado pela fórmula do Acórdão TCU 2.622/2013. Para comparação, o acórdão traz faixas de referência para obras públicas: de 20,34% a 25,00% em construção de edifícios e de 11,10% a 16,80% em fornecimento de materiais e equipamentos. A aba Indiretos e BDI permite BDI diferenciado para materiais. A taxa de tributos depende do regime tributário da empresa.

Atualize a base na aba Base de preços. Para padronizar a equipe, exporte a base em JSON e importe-a nos outros computadores. O botão Restaurar base original desfaz as alterações.

## Limitações conhecidas

A IA pode interpretar cotas, escalas e quantidades de forma errada, sobretudo em fotos inclinadas e desenhos à mão livre. A memória de cálculo de cada insumo existe para permitir essa conferência. Preços de referência são médias: mercado local, volume e condições de pagamento mudam o valor real, e as cotações formais sempre prevalecem. Os índices de HH por tonelada do estimador são parâmetros iniciais e devem ser calibrados com o histórico de obras da Calman.

O site não lê DWG, DXF nem HEIC. PDFs são aceitos até 24 MB, e as imagens são reduzidas para 1.568 pixels no maior lado; detalhes pequenos podem se perder, então fotografe desenhos grandes por partes. O checklist de SST é um apoio e não substitui APR, permissão de trabalho, PGR nem a análise do responsável. A exportação para Excel e a leitura de planilhas e documentos Word usam bibliotecas carregadas de cdn.jsdelivr.net, que precisa estar acessível na rede.

## Solução de problemas

**"A chave da API não foi aceita".** Confira se a chave foi colada inteira, se não foi revogada e se a organização tem créditos.

**"Limite de uso ou de gastos da API atingido".** Aguarde alguns minutos ou revise o limite no Console.

**"Modelo não encontrado".** Em Configurações, clique em Testar conexão e escolha um modelo disponível para a chave.

**Erro que menciona busca web.** Desmarque a pesquisa na internet ou peça ao administrador para habilitá-la no Console.

**"Não foi possível conectar à API".** Verifique a internet e se o firewall ou o proxy da empresa bloqueia api.anthropic.com. Abra o site pelo endereço https do GitHub Pages.

**Aviso de resposta incompleta.** O orçamento atingiu o limite de saída. Aumente o limite em Configurações ou divida o esboço em partes.

**Exportar para Excel não funciona, ou planilhas e documentos Word anexados não são lidos.** A rede está bloqueando cdn.jsdelivr.net.

**O logotipo não aparece.** O arquivo deve se chamar exatamente `logo.png`, em letras minúsculas, e estar na raiz do repositório. Outra opção é carregar o logotipo em Configurações.

**Os orçamentos sumiram.** Os dados do navegador foram limpos ou você está em outro navegador ou computador. Importe a última cópia de segurança.

---

Calman Caldeiraria | Santa Cruz de Minas / 2026
