<template>
  <v-container>
    <div>
      <v-btn @click="toggleModal" v-model="dialog">
        <v-icon left>mdi-plus</v-icon>Novo Opt-In
      </v-btn>
    </div>
    <v-card>
      <v-data-table :headers="headers" :items="modifiedItems">
      </v-data-table>
    </v-card>
  </v-container>
</template>

<script>
export default {
  name: "HomeView",
  computed: {
    modifiedItems() {
      return this.items.map((item) => ({
        ...item,
        paymentScheme: `${item.paymentScheme.code} (${item.paymentScheme.name})`,
      }));
    },
  },
  data() {
    return {
      headers: [
        { text: "Titular", value: "participantDocumentId" },
        { text: "Credenciadora", value: "managedParticipantId" },
        { text: "Arranjo de Pagamento", value: "paymentScheme" },
        { text: "Data de Opt-In", value: "optInSignatureDate" },
        { text: "Início/Término de Vigência", value: "optInStartingDate" },
        { text: "Status", value: "status" },
        { text: "Ações", value: "actions" },
      ],
      items: [
        {
          managedParticipantId: "55.631.202/3229-23",
          requestProtocol: "string",
          recipientDocument: "string",
          participantDocumentId: "12.345.678/0001-01",
          financierDocument: "string",
          paymentScheme: {
            name: "Bandeira A",
            code: "1",
          },
          optInSignatureDate: "03/07/2023",
          optInStartingDate: "03/07/2023",
          optInEndingDate: "03/07/2023",
          domicileIndicator: "string",
          status: false,
        },
        {
          managedParticipantId: "55.631.202/3229-23",
          requestProtocol: "string",
          recipientDocument: "string",
          participantDocumentId: "98.765.432/0001-21",
          financierDocument: "string",
          paymentScheme: {
            name: "Bandeira B",
            code: "1",
          },
          optInSignatureDate: "03/07/2023",
          optInStartingDate: "03/07/2023",
          optInEndingDate: "03/07/2023",
          domicileIndicator: "string",
          status: true,
        },
        {
          managedParticipantId: "55.631.202/3229-23",
          requestProtocol: "string",
          recipientDocument: "string",
          participantDocumentId: "45.678.901/0001-34",
          financierDocument: "string",
          paymentScheme: {
            name: "Bandeira C",
            code: "1",
          },
          optInSignatureDate: "03/07/2023",
          optInStartingDate: "03/07/2023",
          optInEndingDate: "03/07/2023",
          domicileIndicator: "string",
          status: true,
        },
        {
          managedParticipantId: "55.631.202/3229-23",
          requestProtocol: "string",
          recipientDocument: "string",
          participantDocumentId: "12.345.678/0001-01",
          financierDocument: "string",
          paymentScheme: {
            name: "Bandeira A",
            code: "2",
          },
          optInSignatureDate: "03/07/2023",
          optInStartingDate: "03/07/2023",
          optInEndingDate: "03/07/2023",
          domicileIndicator: "string",
          status: true,
        },
        {
          managedParticipantId: "55.631.202/3229-23",
          requestProtocol: "string",
          recipientDocument: "string",
          participantDocumentId: "98.765.432/0001-21",
          financierDocument: "string",
          paymentScheme: {
            name: "Bandeira B",
            code: "3",
          },
          optInSignatureDate: "03/07/2023",
          optInStartingDate: "03/07/2023",
          optInEndingDate: "03/07/2023",
          domicileIndicator: "string",
          status: true,
        },
        {
          managedParticipantId: "55.631.202/3229-23",
          requestProtocol: "string",
          recipientDocument: "string",
          participantDocumentId: "45.678.901/0001-34",
          financierDocument: "string",
          paymentScheme: {
            name: "Bandeira B",
            code: "3",
          },
          optInSignatureDate: "03/07/2023",
          optInStartingDate: "03/07/2023",
          optInEndingDate: "03/07/2023",
          domicileIndicator: "string",
          status: true,
        },
        {
          managedParticipantId: "55.631.202/3229-23",
          requestProtocol: "string",
          recipientDocument: "string",
          participantDocumentId: "12.345.678/0001-01",
          financierDocument: "string",
          paymentScheme: {
            name: "Bandeira A",
            code: "1",
          },
          optInSignatureDate: "03/07/2023",
          optInStartingDate: "03/07/2023",
          optInEndingDate: "03/07/2023",
          domicileIndicator: "string",
          status: true,
        },
        {
          managedParticipantId: "55.631.202/3229-23",
          requestProtocol: "string",
          recipientDocument: "string",
          participantDocumentId: "98.765.432/0001-21",
          financierDocument: "string",
          paymentScheme: {
            name: "Bandeira A",
            code: "1",
          },
          optInSignatureDate: "03/07/2023",
          optInStartingDate: "03/07/2023",
          optInEndingDate: "03/07/2023",
          domicileIndicator: "string",
          status: true,
        },
        {
          managedParticipantId: "55.631.202/3229-23",
          requestProtocol: "string",
          recipientDocument: "string",
          participantDocumentId: "45.678.901/0001-34",
          financierDocument: "string",
          paymentScheme: {
            name: "Bandeira A",
            code: "1",
          },
          optInSignatureDate: "03/07/2023",
          optInStartingDate: "03/07/2023",
          optInEndingDate: "03/07/2023",
          domicileIndicator: "string",
          status: false,
        },
      ],
    };
  },
  methods: {
    toggleModal() {
      this.dialog = !this.dialog
      console.log("Botão clicado!");
    },
    detailsItem(item) {
      console.log("Detalhes do item:", item);
      // Lógica para exibir detalhes do item
    },
    editItem(item) {
      console.log("Editar item:", item);
      // Lógica para editar o item
    },
    deleteItem(item) {
      console.log("Remover item:", item);
      // Lógica para remover o item
      const index = this.items.indexOf(item);
      if (index !== -1) {
        this.items.splice(index, 1);
      }
    },
  },
};
</script>
