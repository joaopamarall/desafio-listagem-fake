<template>
  <v-container>
    <template>
      <v-btn @click="addItem()" v-model="dialog">
        <v-icon left>mdi-plus</v-icon>Novo Opt-In
      </v-btn>
    </template>
    <template>
      <v-dialog v-model="dialog" max-width="800px">
        <v-card>
          <v-card-title>
            <span class="text-h5">{{ formTitle }}</span>
          </v-card-title>

          <v-card-text>
            <v-container>
              <v-row>
                <v-col cols="12" sm="6" md="4">
                  <v-text-field v-model="modifiedItems.managedParticipantId" label="Nome do gerente"></v-text-field>
                </v-col>
                <v-col cols="12" sm="6" md="4">
                  <v-text-field v-model="modifiedItems.requestProtocol" label="Protocolo de solicitação"></v-text-field>
                </v-col>
                <v-col cols="12" sm="6" md="4">
                  <v-text-field v-model="modifiedItems.recipientDocument" label="Documento de recebimento"></v-text-field>
                </v-col>
                <v-col cols="12" sm="6" md="4">
                  <v-text-field v-model="modifiedItems.participantDocumentId" label="Nome do participante"></v-text-field>
                </v-col>
                <v-col cols="12" sm="6" md="4">
                  <v-text-field v-model="modifiedItems.financierDocument" label="Documento financeiro"></v-text-field>
                </v-col>
                <v-col cols="12" sm="6" md="4">
                  <v-text-field v-model="modifiedItems.name" label="Bandeira do cartão"></v-text-field>
                </v-col>
                <v-col cols="12" sm="6" md="4">
                  <v-text-field v-model="modifiedItems.code" label="Código do cartão"></v-text-field>
                </v-col>
                <v-col cols="12" sm="6" md="4">
                  <v-text-field v-model="modifiedItems.optInSignatureDate" label="Data de assinatura"></v-text-field>
                </v-col>
                <v-col cols="12" sm="6" md="4">
                  <v-text-field v-model="modifiedItems.optInStartingDate" label="Data de início"></v-text-field>
                </v-col>
                <v-col cols="12" sm="6" md="4">
                  <v-text-field v-model="modifiedItems.optInEndingDate" label="Data de vencimento"></v-text-field>
                </v-col>
                <v-col cols="12" sm="6" md="4">
                  <v-text-field v-model="modifiedItems.domicileIndicator" label="Indicador de domicílio"></v-text-field>
                </v-col>
              </v-row>
            </v-container>
          </v-card-text>

          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="blue darken-1" text @click="closeModal">
              Cancel
            </v-btn>
            <v-btn color="blue darken-1" text @click="saveItem">
              Save
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </template>
    <template>
      <v-card>
        <v-data-table :headers="headers" :items="modifiedItems">
          <template v-slot:item.actions="{ item }">
            <td>
              <v-icon @click="editItem(item)">mdi-pencil</v-icon>
              <v-icon @click="detailsItem(item)">mdi-eye</v-icon>
              <v-icon @click="deleteItem(item)">mdi-delete</v-icon>
            </td>
          </template>
        </v-data-table>
      </v-card>
    </template>
  </v-container>
</template>

<script>
export default {
  name: "HomeView",
  computed: {
    modifiedItems() {
      return this.items.map((item) => ({
        ...item,
        paymentScheme: item.paymentScheme ? `${item.paymentScheme.code} (${item.paymentScheme.name})` : { name: '', code: '' },
      }));
    },
    formTitle() {
      return this.editedIndex === -1 ? 'New Item' : 'Edit Item'
    },
  },
  data() {
    return {
      dialog: false,
      index: -1,
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
      ],
    };
  },
  methods: {
    toggleModal() {
      this.dialog = !this.dialog
    },
    closeModal() {
      this.dialog = false;
    },
    saveItem() {
      this.toggleModal();
      if (this.index > -1) {
        this.editItem(this.modifiedItems);
        this.closeModal();
      } else {
        this.items.push({ ...this.modifiedItems });
        this.closeModal();
      }

    },
    addItem() {
      this.toggleModal();
    },
    editItem(item) {
      this.toggleModal();
    },
    detailsItem(item) {
      this.toggleModal();
    },
    deleteItem(item) {
      const index = this.items.indexOf(item);
      if (index !== -1) {
        this.items.splice(index, 1);
      }
    },
  },
};
</script>
