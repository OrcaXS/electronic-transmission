<template>
  <p>
    You're now connecting to Transmission {{ address }}
  </p>
</template>

<script>
  // import os from 'os';
  const rp = require('request-promise');

  let options = {
    simple: false,
    resolveWithFullResponse: true,
    headers: {
      'x-transmission-session-id': 'id',
    },
    uri: '',
    method: 'POST',
    json: true,
    set setbody(parser) {
      this.body = parser;
    },
    set setid(id) {
      this.headers['x-transmission-session-id'] = id;
    },
  };

  let getTorrentInfo = {
    arguments: {
      fields: [
        'id',
        'name',
        'totalSize',
      ],
      ids: [
        1,
      ],
    },
    method: 'torrent-get',
    tag: 39693,
  };

  let sessionIDParser = {
    method: 'session-get',
    tag: 12345,
  };

  function getSessionID() {
    options.setbody = sessionIDParser;
    return rp(options)
    .then(body => {
      return body.statusCode === 409 ? body.headers['x-transmission-session-id'] : 'err';
    })
    .catch(function (err) {
      console.log(err);
    });
  }

  function postRequest(args, sessionID) {
    options.setid = sessionID;
    options.setbody = args;
    return rp(options)
    .then(function (body) {
      console.log(body.body);
    })
    .catch(function (err) {
      console.log(err);
    });
  }

  export default {
    data() {
      return {
        address: '127.0.0.1',
      };
    },
  };
</script>
