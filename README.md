{
  "name": "stremio-addon",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  },
  "dependencies": {
    "stremio-addon-sdk": "^1.6.10"
  }
}const { addonBuilder } = require("stremio-addon-sdk");

const manifest = {
  id: "org.faselhd.final",
  version: "1.0.0",
  name: "FaselHD Movies",
  description: "The Nun (2018) بث مباشر",
  resources: ["catalog", "stream"],
  types: ["movie"],
  catalogs: [
    {
      type: "movie",
      id: "fasel_movies",
      name: "Fasel Movies"
    }
  ]
};

const builder = new addonBuilder(manifest);

// 🎬 الكتالوج
builder.defineCatalogHandler(() => ({
  metas: [
    {
      id: "the_nun_2018",
      type: "movie",
      name: "The Nun",
      year: 2018,
      poster: "https://image.tmdb.org/t/p/w500/sFC1ElvoKGdHJIWRpNB3xWJ9lJA.jpg"
    }
  ]
}));

// ▶️ روابط المشاهدة
builder.defineStreamHandler(({ id }) => {
  if (id === "the_nun_2018") {
    return {
      streams: [
        {
          title: "HD",
          url: "https://36x8fqcfqsv376o2c3bj.streamnruby.net/hls2/02/00050/bb9e64dhOrjp_l,n,h,.urlset/master.m3u8?t=7s6RN22z01BixaQH1THP2iwcYY7GP-eURaTM7tDxOV/O&s=1767372872&e=324008v=1502915664&i=2a01:9700:461d:400&sp=0GET"
        }
      ]
    };
  }
  return { streams: [] };
});

module.exports = builder.getInterface();