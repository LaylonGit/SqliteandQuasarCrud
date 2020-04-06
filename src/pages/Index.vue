<template>
  <q-page class="flex flex-center">
    <q-btn label="Monta banco" @click="montabanco()"/>
    <q-btn label="Monta tbl" @click="criandotabela()"/>
    <q-btn label="pega dados" @click="pegandodados()"/>

  </q-page>
</template>

<script>
export default {
  data () {
    return {
      db: ''
    }
  },
  methods: {
    montabanco () {
      this.db = window.sqlitePlugin.openDatabase({
        name: 'my.db',
        location: 'default',
        androidDatabaseProvider: 'system'
      })
      console.log(this.db)
    },
    criandotabela () {
      this.montabanco()
      this.db.transaction(function (tx) {
        tx.executeSql('CREATE TABLE IF NOT EXISTS DemoTable (name, score)')
        tx.executeSql('INSERT INTO DemoTable VALUES (?1,?2)', ['Alice', 101])
        tx.executeSql('INSERT INTO DemoTable VALUES (?1,?2)', ['paulo', 2002])
      }, function (error) {
        console.log('Transaction ERROR: ' + error.message)
      }, function () {
        console.log('Populated database OK')
      })
    },
    pegandodados () {
      this.montabanco()
      this.db.transaction(function (tx) {
        tx.executeSql('SELECT name AS allnames FROM DemoTable', [], function (tx, rs) {
          // for (var i = 0; rs.rows !== undefined; i++) {
          console.log(rs.rows)
          // }
        }, function (tx, error) {
          console.log('SELECT error: ' + error.message)
        })
      })
    }
  }
}
</script>
