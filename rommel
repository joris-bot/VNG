const SYSTEM_SUFFIX = `

Sluit elk antwoord altijd af met een sectie "📚 Bronnen:" waarin je de wet- en regelgeving, beleidsprogramma's of publicaties noemt waarop je antwoord is gebaseerd. Gebruik dit formaat:

📚 Bronnen:
• [naam van wet, artikel of programma]
• [naam van wet, artikel of programma]

Voorbeelden van bronnen die je kunt noemen: Omgevingswet, Woningwet, Bro, Wro, Nationale Woon- en Bouwagenda, Woningbouwimpuls, Rijksprogramma Woningbouw, VNG-ledenbrief, CBS Woononderzoek, PBL Rapport. Wees zo specifiek mogelijk (bijv. "Omgevingswet art. 5.1" of "Woningwet art. 47"). Als je niet zeker bent van een specifieke bron, vermeld dan alleen bronnen waarvan je redelijk zeker bent.`;

exports.handler = async (event) => {
  if (event.httpMethod === "OPTIONS") {
    return {
      statusCode: 204,
      headers: {
        "Access-Control-Allow-Origin": "*",
        "Access-Control-Allow-Methods": "POST, OPTIONS",
        "Access-Control-Allow-Headers": "Content-Type",
      },
      body: "",
    };
  }

  if (event.httpMethod !== "POST") {
    return { statusCode: 405, body: "Method not allowed" };
  }

  const body = JSON.parse(event.body);

  const response = await fetch("https://api.anthropic.com/v1/messages", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      "x-api-key": process.env.ANTHROPIC_API_KEY,
      "anthropic-version": "2023-06-01",
    },
    body: JSON.stringify({
      model: "claude-sonnet-4-6",
      max_tokens: 2048,
      system: body.system + SYSTEM_SUFFIX,
      messages: body.messages,
    }),
  });

  const data = await response.json();

  return {
    statusCode: response.status,
    headers: {
      "Content-Type": "application/json",
      "Access-Control-Allow-Origin": "*",
    },
    body: JSON.stringify(data),
  };
};
