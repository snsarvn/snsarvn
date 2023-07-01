const axios = require('axios');
const fs = require("fs");

const limit = 1;
const apiURL = `https://api.api-ninjas.com/v1/jokes?limit=${limit}`;

const getQuote = async () => {
  try {
    const response = await axios.get(apiURL, {
      headers: {
        'X-Api-Key': 'iemkezsN5DXWbWCaGxZU2g==VWckCXz0dmoeK9Ux'
      }
    })
    const joke = response.data[0].joke;


    console.log("new joke", `"${joke}"`);

    return {
      joke,
    };
  } catch (err) {
    console.error(err.message);
    return {};
  }
};

const generate = async () => {
  const { joke } = await getQuote();

  if (!joke) return;

  fs.writeFileSync("README.md", `_**${joke}**_\n\n`);
};

generate();
