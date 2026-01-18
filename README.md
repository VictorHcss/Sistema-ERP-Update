# Sistema ERP Web (PHP + JavaScript)

## Resumo
Este projeto implementa um Sistema ERP web para gestão de clientes, produtos, vendas e estoque. O objetivo é oferecer um ambiente didático e funcional, com foco em boas práticas de integração PHP–JavaScript, visualização de dados com Chart.js e organização modular de interfaces e controladores.

## Objetivos
- Organizar informações operacionais (clientes, produtos, vendas, estoque) em uma aplicação web.
- Demonstrar integração entre PHP (backend) e JavaScript (frontend).
- Apresentar indicadores e gráficos de desempenho usando Chart.js.
- Servir como base acadêmica para estudos de arquitetura web, integração de dados e UX.

## Escopo
- Módulos: Clientes, Produtos, Vendas, Estoque, Dashboard.
- Dashboard com cartões de resumo e dois gráficos principais:
  - Ranking de Vendedores
  - Atingimento de Meta do Mês
- Autenticação básica (MVP) no frontend e integração com dados do backend em páginas PHP específicas.

## Tecnologias
- PHP (PDO) e HTML/CSS
- JavaScript (ES6) com organização por namespace de aplicação
- Chart.js (CDN)
- Ambiente recomendado: XAMPP (Apache + PHP + MySQL)

## Arquitetura
- Camada de apresentação (views) em PHP, com injeção de dados no frontend via variáveis globais:
  - `window.rankingNomes`, `window.rankingValores`, `window.percentualMeta`
- Lógica de UI e controladores em JavaScript:
  - [main.js](file:///c:/xampp/htdocs/sistemaerp/js/main.js): App.UI, App.Controllers, App.Data, App.Auth e App.Router
- Estilização centralizada:
  - [style.css](file:///c:/xampp/htdocs/sistemaerp/css/style.css)
- Componentização de navegação:
  - [header.php](file:///c:/xampp/htdocs/sistemaerp/includes/header.php)
- Página principal e orquestração de scripts:
  - [index.php](file:///c:/xampp/htdocs/sistemaerp/index.php)

### Organização do Código (Frontend)
- `window.App` agrupa responsabilidades:
  - `UI`: recursos visuais, modais, toasts e renderização de gráficos
  - `Controllers`: orquestra lógica por página/módulo
  - `Data`: operações localStorage (MVP didático)
  - `Auth`: autenticação simples no cliente (MVP)
  - `Router`: roteamento básico por pathname

## Estrutura de Diretórios (resumo)
- `index.php` — Dashboard e injeção de dados globais
- `includes/header.php` — Sidebar e navegação
- `css/style.css` — Estilos
- `js/main.js` — Lógica da aplicação (UI, Controllers, etc.)
- `modules/clients/clients.php` — Gestão de clientes
- `modules/products/products.php` — Gestão de produtos
- `modules/sales/sales.php` — Gestão de vendas
- `modules/stock/stock.php` — Gestão de estoque

## Requisitos
- XAMPP (ou equivalente): Apache, PHP 7.4+ (recomendado), MySQL
- Extensão PDO habilitada
- Acesso a `htdocs` para publicação local

## Instalação
1. Copie o diretório `sistemaerp` para `c:\xampp\htdocs\` (Windows).
2. Configure o banco de dados (credenciais e conexão) conforme seus arquivos PHP.
3. Garanta que a sessão do usuário esteja ativa e que as consultas utilizem `company_id` quando aplicável.
4. Inicie o Apache e o MySQL pelo XAMPP.
5. Acesse `http://localhost/sistemaerp/`.

## Configuração de Scripts
- Ordem de scripts no final do [index.php](file:///c:/xampp/htdocs/sistemaerp/index.php):
  1. Chart.js (CDN)
  2. Bloco `<script>` com injeção de dados do PHP em `window.*`
  3. `js/main.js` (carregado por último)
  4. Chamada opcional para inicializar gráficos imediatamente:
     ```html
     <script>
       if (window.App?.UI?.renderDashboardCharts) {
         window.App.UI.renderDashboardCharts([], []);
       }
     </script>
     ```

## Fluxos Principais
- Dashboard:
  - Preenchimento dos cards via `Controllers.dashboard` com validações de elementos:
    - `#totalClients`, `#totalProducts`, `#totalSales`, `#totalStock`
  - Gráficos:
    - Ranking de Vendedores: usa `window.rankingNomes || []` e `window.rankingValores || []`
    - Meta do Mês: usa `window.percentualMeta || 0` e `100 - window.percentualMeta`
  - Verificação de existência dos canvas antes de renderizar (`document.getElementById`).

## Boas Práticas Aplicadas
- Verificação de elementos DOM antes de manipulação
- Fallbacks defensivos para variáveis globais
- Separação de responsabilidades por namespaces
- Evitar múltiplas inclusões de `main.js` para prevenir conflitos de identificadores

## Testes e Validação
- Testes manuais recomendados:
  - Carregamento do Dashboard sem erros de console
  - Presença de dados nos cards e gráficos
  - Navegação pelos módulos sem quebra
  - Logout e mudanças de estado no menu
- Integração com testes automatizados (opcional) pode ser adicionada conforme o stack do curso/disciplinas.

## Limitações
- Parte da autenticação e persistência é demonstrativa via `localStorage` (MVP).
- O schema de banco e camadas de serviço podem variar conforme o ambiente do aluno.

## Trabalhos Futuros
- Implementar autenticação e autorização completas no backend
- Camada de serviços/DTOs para desacoplar o frontend
- Testes automatizados (PHPUnit, Jest/Vitest, etc.)
- Observabilidade (logs, métricas) e tratamento de falhas

## Referências
- PHP Manual: https://www.php.net/manual/pt_BR/
- PDO: https://www.php.net/pdo
- Chart.js: https://www.chartjs.org/docs/latest/
- MDN Web Docs (DOM/JS): https://developer.mozilla.org/

## Licença
Projeto de uso acadêmico. Licença a definir conforme a disciplina/instituição.

## Autores
- Victor H

