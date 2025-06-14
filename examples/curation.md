# Curation

**Este arquivo centraliza todos os dados de curadoria que alimentam os selects e campos de tags dos formulários, conforme a estória `TFLOW-011`.**

``` JSON
{
  "professionalAreas": [
    { "id": "area_1", "name": "Desenvolvimento de Software" },
    { "id": "area_2", "name": "Design de Produto (UX/UI)" },
    { "id": "area_3", "name": "Ciência de Dados" },
    { "id": "area_4", "name": "Gestão de Produtos" },
    { "id": "area_5", "name": "DevOps / SRE" },
    { "id": "area_6", "name": "Qualidade de Software (QA)" }
  ],
  "experienceLevels": [
    { "id": "level_1", "name": "Estágio", "order": 1 },
    { "id": "level_2", "name": "Júnior", "order": 2 },
    { "id": "level_3", "name": "Pleno", "order": 3 },
    { "id": "level_4", "name": "Sênior", "order": 4 },
    { "id": "level_5", "name": "Especialista / Principal", "order": 5 }
  ],
  "languageList": [
    { "id": "lang_1", "name": "Português" },
    { "id": "lang_2", "name": "Inglês" },
    { "id": "lang_3", "name": "Espanhol" },
    { "id": "lang_4", "name": "Francês" },
    { "id": "lang_5", "name": "Alemão" }
  ],
  "proficiencyLevels": [
    { "id": "prof_1", "name": "Básico (A1/A2)", "order": 1 },
    { "id": "prof_2", "name": "Intermediário (B1)", "order": 2 },
    { "id": "prof_3", "name": "Avançado (B2)", "order": 3 },
    { "id": "prof_4", "name": "Fluente (C1/C2)", "order": 4 },
    { "id": "prof_5", "name": "Nativo ou Bilíngue", "order": 5 }
  ],
  "softSkills": [
    { "id": "ss_1", "name": "Liderança Técnica", "description": "Capacidade de guiar tecnicamente a equipe." },
    { "id": "ss_2", "name": "Resolução de Problemas Complexos", "description": "Habilidade para analisar e resolver problemas multifacetados." },
    { "id": "ss_3", "name": "Comunicação", "description": "Habilidade de transmitir ideias de forma clara e eficaz." },
    { "id": "ss_4", "name": "Pensamento Crítico", "description": "Capacidade de analisar informações de forma objetiva e fazer um julgamento fundamentado." },
    { "id": "ss_5", "name": "Visão Estratégica", "description": "Capacidade de alinhar decisões técnicas com os objetivos do negócio." },
    { "id": "ss_6", "name": "Negociação", "description": "Habilidade para chegar a acordos e alinhar stakeholders." }
  ],
  "technologies": [
    { "id": "tech_1", "name": "Kotlin", "type": "Linguagem de Programação" },
    { "id": "tech_2", "name": "Java", "type": "Linguagem de Programação" },
    { "id": "tech_3", "name": "Python", "type": "Linguagem de Programação" },
    { "id": "tech_4", "name": "TypeScript", "type": "Linguagem de Programação" },
    { "id": "tech_5", "name": "Angular", "type": "Framework Frontend" },
    { "id": "tech_6", "name": "Spring Boot", "type": "Framework Backend" },
    { "id": "tech_7", "name": "Kafka", "type": "Mensageria" },
    { "id": "tech_8", "name": "AWS", "type": "Plataforma de Cloud" },
    { "id": "tech_9", "name": "Docker", "type": "Conteinerização" },
    { "id": "tech_10", "name": "Figma", "type": "Ferramenta de Design" },
    { "id": "tech_11", "name": "Jira", "type": "Ferramenta de Gestão" },
    { "id": "tech_12", "name": "Terraform", "type": "Infraestrutura como Código" },
    { "id": "tech_13", "name": "PostgreSQL", "type": "Banco de Dados" }
  ]
}
```