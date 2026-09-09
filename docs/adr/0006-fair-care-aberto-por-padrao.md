# Aberto por padrão, com autoridade cultural indígena modelada via Local Contexts

"Acesso amplo e irrestrito" significa **irrestrito por padrão, não irrestrito sem exceção**. A formulação adotada é a do guia *Guidance for Indigenous Collections and Indigenous Data* (Anderson, Hudson, Hopkins, Roe & Smith, 2026 — Creative Commons + Local Contexts, [DOI 10.5281/zenodo.21071544](https://doi.org/10.5281/zenodo.21071544)):

> "cultural heritage should be as open as possible and as closed as necessary"

A arquitetura adota as recomendações desse guia como normativas para todo dado de coleção e de espécie com conhecimento tradicional associado.

## Três eixos de sensibilidade, três mecanismos

| Eixo | Mecanismo | Quem decide |
|---|---|---|
| Localidade de táxon sob pressão de coleta ilegal | **Generalização** de coordenadas (célula, não supressão) — o dado permanece publicável e analiticamente útil | Curadoria + autoridade ambiental |
| Conhecimento tradicional associado (nomes, usos, classificações etnozoológicas) | **TK Labels** definidas pela comunidade; entidade separada do registro de ocorrência | **A comunidade detentora** |
| Espécime, amostra genética e sequência de origem indígena ou coletados em território indígena | **BC (Biocultural) Labels** — desenhadas pelo Local Contexts precisamente para coleções biológicas e amostras genéticas | **A comunidade detentora** |

Conhecimento tradicional **nunca** é ingerido como campo comum do registro de ocorrência (por exemplo, um `vernacularName` qualquer): isso transferiria tacitamente a titularidade da comunidade para o publicador. Base normativa: princípios CARE (Carroll et al. 2020), UNDRIP Art. 31, Protocolo de Nagoya e Lei 13.123/2015.

## Labels e Notices: quem aplica o quê

Correção deliberada a um erro de modelagem comum — a instituição **não** classifica a sensibilidade cultural do dado:

- **TK e BC Labels** são aplicadas **pela comunidade**, expressam autoridade cultural, e seu texto é **customizável pela própria comunidade**. Existem 30 Labels em três categorias: *Provenance*, *Protocols*, *Permissions*.
- **Notices** são aplicados **pela instituição ou pesquisador** e apenas *reconhecem* a existência de direitos indígenas. São três: **Engagement** (*Open to Collaborate*), **Disclosure** (TK/BC Notice, que funciona como *placeholder* até a comunidade aplicar sua Label) e **Collections Care** (para acervos que exigem cuidado cultural *in situ*).

Consequência de projeto: o sistema precisa de um **agente Comunidade** com autoridade de escrita própria, distinto do curador e do pesquisador do [ADR 0004](./0004-autoridade-de-assercao.md). A comunidade não "propõe para aprovação" — ela é a autoridade final sobre suas Labels.

## Integração técnica

- **Local Contexts Hub** é o sistema de registro das Labels e Notices, com identificadores permanentes e API aberta. O sistema **não replica nem congela** o texto das Labels: resolve-as pelo identificador contra o Hub, porque a comunidade pode revisar o texto a qualquer momento e uma cópia local envelhecida reintroduz exatamente a apropriação que a Label combate.
- O **LC Project ID** é gravado no campo `rights` do registro (prática recomendada pelo guia para Dublin Core e **Darwin Core**, conforme a orientação estabelecida com o DataCite).
- **CC Licenses e LC Labels coexistem** e compartilham o mesmo campo de metadado: licenças expressam direitos autorais, Labels expressam direitos culturais. Tensão aparente entre uma licença e uma Label (por exemplo, `CC BY` frente a *TK Community Use Only*) não é conflito técnico a resolver por regra — é sinal de que a expectativa da comunidade nunca esteve no registro, e se resolve por diálogo.
- Adoção do **Indigenous Metadata Bundle** (Taitingfong et al. 2023) como referência para os campos de metadado indígena, atendendo à recomendação "use content management systems that include fields for Indigenous metadata".

## As cinco áreas de ação como requisitos

O guia organiza a prática em cinco áreas; cada uma gera requisito arquitetural:

| Área | Requisito no sistema |
|---|---|
| **Acknowledgment** | Registro explícito de território e comunidade de origem do espécime, mesmo quando a proveniência é incompleta |
| **Attribution** | *Attribution Incomplete Notice* aplicável a registros históricos de proveniência duvidosa — a lacuna é declarada, não silenciada |
| **Authorship** | Coautoria e afiliação comunitária como dados citáveis, não texto livre |
| **Access** | Campos de metadado indígena nativos; política de acesso por acervo; contato institucional publicado |
| **Authority** | Agente Comunidade com poder de escrita sobre suas Labels, sem intermediação da curadoria |

## Considered Options

- **Irrestrito sem exceções**: coerente com FAIR em estado puro, mas viola CARE, UNDRIP e a legislação brasileira de acesso ao patrimônio genético e ao conhecimento tradicional associado.
- **Acesso graduado por perfil de consumidor**: rejeitado por ser um sistema de permissões vestido de princípio ético — impõe burocracia sobre a totalidade dos dados para proteger uma fração, e transfere à instituição uma decisão que é da comunidade.
- **Sensibilidade classificada pela curadoria**: rejeitado após leitura do guia. Reproduz a estrutura colonial que o instrumento existe para desfazer.

## Consequências

- Generalização de táxon e generalização de território são independentes e podem incidir sobre o mesmo registro.
- O Darwin Core Archive publicado e a API expõem o **fato** da generalização (`informationWithheld`, `dataGeneralizations`) e o LC Project ID em `rights` — nunca omitem silenciosamente.
- Dependência externa deliberada do Local Contexts Hub para resolução de Labels; indisponibilidade do Hub degrada a exibição da Label, e nunca a converte em ausência de restrição.
- Digitalização e publicação abertas deixam de ser o padrão automático para material de origem indígena: passam a requerer consentimento livre, prévio e informado.
