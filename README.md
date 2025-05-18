# imersao.ia-gemini
Projeto Final do Curso Imersão IA – Google Gimini e Alura

Projeto "MentorIA Curricular: Seu currículo alinhado ao futuro do mercado”. 

"Com MentorIA Curricular, use multiagentes de IA para criar ou otimizar o currículo do seu curso, alinhando-o às demandas do mercado e à concorrência. Estudantes também podem validar a relevância da sua formação."

graph TD 

    A [Início: Input do Usuário<br>(Currículo do Curso Alvo, Área de Estudo, Concorrentes Opcionais)] --> B(Agente Orquestrador);

    B -- Detalhes do Curso Alvo --> C(1. Agente Analista de Currículo Alvo);
    C -- Estrutura e Habilidades do Currículo Alvo --> F;

    B -- Área de Estudo --> D(2. Agente de Inteligência de Mercado);
    D -- Demandas e Habilidades do Mercado --> F;

    B -- Nomes/Links de Concorrentes<br>OU Área de Estudo para Busca --> E(3. Agente Analista de Concorrência);
    E -- Currículos e Habilidades dos Concorrentes --> F;

    F(4. Agente de Mapeamento e Diagnóstico Comparativo) -- Análise Cruzada e Identificação de Gaps/Forças --> G(5. Agente Gerador de Relatório e Recomendações);
    G -- Relatório Detalhado e Sugestões --> B;
    B -- Output Final --> H[Fim: Relatório Analítico para o Usuário]; 


1. Agente Analista de Currículo Alvo (Target Curriculum Analyst Agent)
   - Responsabilidade Principal: Processar e dissecar o currículo do curso que será analisado.
   - Tarefas:
       - Receber o documento do currículo (PDF, DOC, URL) ou texto.
       - Extrair a estrutura do curso: disciplinas, módulos, carga horária por disciplina.
       - Identificar os objetivos de aprendizado declarados.
       - Extrair as competências e habilidades que o currículo afirma desenvolver.
       - Identificar tecnologias, ferramentas ou metodologias específicas mencionadas.
   - Como Gemini pode ajudar: 
        - Processamento de Documentos: Utilizar modelos Gemini com capacidade de entender e extrair informações de documentos (PDFs, texto).
        - Extração de Entidades Nomeadas (NER): Identificar e classificar "disciplinas", "habilidades", "tecnologias", "objetivos". Por exemplo, extrair "Python", "Machine Learning", "Análise de Dados" como habilidades/tecnologias de ementas.
        - Análise de Conteúdo: Interpretar ementas e descrições de disciplinas para inferir habilidades implícitas.
   - Output: Um objeto estruturado (ex: JSON) contendo a decomposição do currículo alvo, suas disciplinas, e as habilidades/competências associadas.

3. Agente de Inteligência de Mercado (Job Market Intelligence Agent)
   - Responsabilidade Principal: Pesquisar e analisar as demandas atuais do mercado de trabalho para a área do curso.
   - Tarefas:
       - Com base na área do curso (ex: "Ciência de Dados", "Desenvolvimento Web Full-Stack"), pesquisar vagas de emprego recentes.
       - Analisar descrições de vagas para identificar as habilidades técnicas (hard skills) e comportamentais (soft skills) mais requisitadas.
       - Identificar as tecnologias, ferramentas e plataformas mais demandadas.
       - Mapear tendências emergentes e conhecimentos valorizados.
   - Como Gemini pode ajudar:
       - Busca e Coleta de Dados: Se integrado com ferramentas de busca (via function calling/plugins, se disponível no ambiente do desafio), pode buscar em sites de emprego, artigos da indústria, relatórios de tendências.
       - Processamento de Linguagem Natural (PLN): Analisar grandes volumes de texto de descrições de vagas para extrair as habilidades e tecnologias mais frequentes e relevantes.
       - Sumarização e Identificação de Padrões: Consolidar as informações coletadas, identificar padrões de demanda e resumir as principais competências exigidas pelo mercado.
       - Análise de Sentimento/Tópicos: Entender quais são os tópicos mais "quentes" ou valorizados no mercado.
   - Output: Um relatório ou objeto estruturado (ex: JSON) com a lista de habilidades, tecnologias, e tendências do mercado, possivelmente com um ranking de demanda.

5. Agente Analista de Concorrência (Competitor Analyst Agent)
   - Responsabilidade Principal: Coletar e analisar informações sobre os currículos de cursos concorrentes diretos.
   - Tarefas:
       - Identificar os principais cursos concorrentes (se não fornecido, pode tentar buscar com base na área e nível do curso).
       - Coletar informações sobre os currículos desses concorrentes (estrutura, disciplinas, foco, habilidades declaradas).
       - Analisar os pontos fortes e diferenciais de cada concorrente.
   - Como Gemini pode ajudar:
       - Busca e Extração Web: Acessar websites de instituições de ensino para coletar dados curriculares.
       - Processamento de Documentos/Web: Similar ao "Agente Analista de Currículo Alvo", processar os currículos dos concorrentes.
       - Análise Comparativa Preliminar: Identificar as principais disciplinas e habilidades oferecidas pelos concorrentes para facilitar a comparação posterior.
   - Output: Um conjunto de dados estruturados (ex: lista de JSONs), cada um representando a análise de um currículo concorrente.

6. Agente de Mapeamento e Diagnóstico Comparativo (Comparative Mapping and Diagnostic Agent)
   - Responsabilidade Principal: O cérebro analítico do sistema. Realizar o cruzamento das informações coletadas pelos outros agentes.
   - Tarefas:
       - Comparar as habilidades desenvolvidas pelo currículo alvo com as habilidades demandadas pelo mercado (identificadas pelo Agente de Inteligência de Mercado).
           - Identificar GAPs: Habilidades demandadas pelo mercado, mas não cobertas (ou pouco cobertas) pelo currículo.
           - Identificar Excedentes: Habilidades cobertas pelo currículo, mas com baixa demanda no mercado.
           - Identificar Pontos Fortes: Habilidades bem cobertas e em alta demanda.
           - Comparar o currículo alvo com os currículos dos concorrentes.
           - Identificar diferenciais positivos (onde o curso alvo é melhor/mais completo).
           - Identificar desvantagens (onde os concorrentes oferecem algo que o curso alvo não tem).
           - Analisar o alinhamento geral de cada curso com as demandas do mercado.
   - Como Gemini pode ajudar:
       - Raciocínio e Análise Lógica: Comparar listas de habilidades, identificar sobreposições e diferenças.
       - Análise Semântica: Entender que "Desenvolvimento Ágil" e "Scrum" estão relacionados, mesmo que escritos de forma diferente. Modelos de embedding podem ser úteis para calcular similaridade semântica entre descrições de habilidades.
       - Geração de Insights: A partir das comparações, gerar insights sobre o posicionamento do curso.
   - Output: Uma análise detalhada contendo os GAPs, pontos fortes, comparação com concorrentes e o nível de aderência ao mercado.

8. Agente Gerador de Relatório e Recomendações (Report and Recommendation Generation Agent)
   - Responsabilidade Principal: Sintetizar todas as análises em um relatório final compreensível e acionável.
   - Tarefas:
       - Estruturar um relatório claro, com seções distintas (aderência ao mercado, análise de competências, comparativo com concorrência).
       - Apresentar os achados de forma visual ou textual clara (gráficos poderiam ser uma extensão, mas um bom texto já é valioso).
       - Gerar recomendações concretas para aprimoramento do currículo alvo, como:
           - Sugestão de inclusão de novas disciplinas/tópicos.
           - Atualização de ementas existentes.
           - Ênfase em certas habilidades.
           - Possíveis nichos de mercado a explorar.
   - Como Gemini pode ajudar:
       - Geração de Texto Avançada: Redigir o relatório final de forma coesa, profissional e persuasiva, utilizando as informações fornecidas pelo "Agente de Mapeamento e Diagnóstico".
       - Sumarização: Resumir os pontos chave da análise.
       - Geração de Recomendações: Com base nos GAPs e oportunidades identificadas, Gemini pode ser instruído (via prompt engineering) a sugerir melhorias específicas e justificar essas sugestões.
   - Output: O relatório final para o usuário.

Agente Orquestrador (Opcional, mas recomendado): 
   - Embora não seja um "agente de IA" no mesmo sentido dos outros, você precisará de um componente central (que pode ser um script Python principal) para:
       - Gerenciar o fluxo de trabalho.
       - Receber o input inicial.
       - Chamar cada agente na ordem correta.
       - Passar os dados de output de um agente como input para o próximo.
       - Formatar e apresentar o resultado final.
