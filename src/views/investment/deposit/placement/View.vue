<template>
  <div class="intro-y flex flex-col sm:flex-row items-center mt-8">
    <h2 class="text-lg font-medium mr-auto" data-cy="title-page">
      Deposit Placement Details
    </h2>
  </div>

  <div
    class="intro-y box lg:mt-5 flex-col"
    v-if="deposit._id && deposit.dueDate"
  >
    <div class="w-full items-center">
      <div
        class="p-5 w-full border-b border-slate-200/60 dark:border-darkmode-400"
      >
        <div class="w-full mb-8">
          <div
            class="pt-4 grid grid-cols-2 md:grid-cols-4 gap-5"
            v-if="deposit.createdAt && deposit.createdBy"
          >
            <div>
              <table class="border-collapse border border-slate-400 w-full">
                <tbody>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Form Number
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-center"
                    >
                      {{ deposit.number }}
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Created At
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-center"
                    >
                      {{ format(new Date(deposit.createdAt), "yyyy/MM/dd") }}
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Created By
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-center"
                    >
                      {{ deposit.createdBy.name || "-" }}
                    </td>
                  </tr>
                  <tr v-if="deposit.deletedBy">
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Deleted At
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-center"
                    >
                      {{
                        deposit.deletedAt
                          ? format(new Date(deposit.deletedAt), "yyyy/MM/dd")
                          : "-"
                      }}
                    </td>
                  </tr>
                  <tr v-if="deposit.deletedBy">
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Deleted By
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-center"
                    >
                      {{ deposit.deletedBy.name || "-" }}
                    </td>
                  </tr>
                  <tr v-if="deposit.deletedBy">
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Deleted Reason
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-center"
                    >
                      {{ deposit.deleteReason || "-" }}
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
            <div class="flex flex-col justify-end items-end h-full">
              <div class="flex flex-row gap-4 justify-start items-end mb-8">
                <button
                  class="bg-orange-500 hover:bg-orange-700 text-white font-bold py-2 px-4 rounded capitalize"
                >
                  {{ deposit.formStatus }}
                </button>
              </div>
              <div
                class="flex flex-row gap-4 justify-end items-end"
                v-if="!deposit.deletedBy && !deposit.renewal_id"
              >
                <button
                  class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
                  @click="onClickDelete()"
                >
                  Delete
                </button>
                <button
                  class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
                  @click="onClickEdit()"
                >
                  Edit
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="w-full items-center">
      <div
        class="p-5 w-full border-b border-slate-200/60 dark:border-darkmode-400"
      >
        <div class="w-full mb-8">
          <h2
            class="font-medium text-lg pb-2 border-b border-slate-200/60 dark:border-darkmode-400"
          >
            Placement Information
          </h2>
          <div class="overflow-x-auto">
            <div class="pt-4 grid grid-cols-1 md:grid-cols-2 gap-5">
              <table class="border-collapse border border-slate-400 w-full">
                <tbody>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Placement Date
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      {{ format(deposit.date, "yyyy/MM/dd") }}
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Bilyet Number
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      {{ deposit.bilyetNumber }}
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Bank
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      {{ deposit.bank.name }}
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Account
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      {{ deposit.account.name }}
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Owner
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      {{ deposit.owner.name }}
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Base Date
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      {{ deposit.baseDate }} Days
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Tenor
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      {{ deposit.tenor }} Days
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Due Date
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      {{ format(deposit.dueDate, "yyyy/MM/dd") }}
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Interest Rollover
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      {{ deposit.isRollOver ? "Yes" : "No" }}
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Amount of Placement
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Rp. {{ numberFormat(deposit.amount) }}
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Bank Source of Fund
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      {{ deposit.sourceBank.name }}
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Bank Account
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      {{ deposit.sourceBankAccount.name }}
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Interest Recipient Bank
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      {{ deposit.recipientBank.name }}
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Interest Recipient Bank Account
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      {{ deposit.recipientBankAccount.name }}
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Payment Method
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      {{
                        deposit.paymentMethod === "advance"
                          ? "Advance"
                          : "In Arrear"
                      }}
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Interest Rate
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      {{ deposit.interestRate }}%
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Amount of Interest (gross)
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Rp. {{ numberFormat(deposit.grossInterest || 0) }}
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Tax Rate
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      {{ deposit.taxRate }}%
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Amount of Tax
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Rp. {{ numberFormat(deposit.taxAmount || 0) }}
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Amount of Interest (net)
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Rp. {{ numberFormat(deposit.netInterest || 0) }}
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Cashback Availability
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      {{ deposit.isCashback ? "Yes" : "No" }}
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>

        <div
          class="w-full mb-8"
          v-if="deposit.returns && deposit.returns.length > 0"
        >
          <h2
            class="font-medium text-lg pb-2 border-b border-slate-200/60 dark:border-darkmode-400"
          >
            Return Information
          </h2>
          <div
            class="overflow-x-auto"
            v-for="(item, index) in deposit.returns || []"
            :key="index"
          >
            <div class="pt-4 grid grid-cols-1 md:grid-cols-2 gap-5">
              <table class="border-collapse border border-slate-400 w-full">
                <tbody>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Base Days
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      {{ item.baseDays || 0 }} Days
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Due Date
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      {{
                        item.dueDate ? format(item.dueDate, "dd/MM/yyyy") : "-"
                      }}
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Interest Rate
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      {{ deposit.interestRate }}%
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Amount of Interest (gross)
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Rp. {{ numberFormat(item.gross || 0) }}
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Tax Rate
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      {{ deposit.taxRate }}%
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Amount of Tax
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Rp. {{ numberFormat(item.taxAmount || 0) }}
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Amount of Interest (net)
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Rp. {{ numberFormat(item.net || 0) }}
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>

        <div
          class="w-full mb-8"
          v-if="deposit.isCashback && deposit.isCashback === true"
        >
          <h2
            class="font-medium text-lg pb-2 border-b border-slate-200/60 dark:border-darkmode-400"
          >
            Cashback Information
          </h2>
          <div
            class="overflow-x-auto"
            v-for="(item, index) in deposit.cashbacks || []"
            :key="index"
          >
            <div class="pt-4 grid grid-cols-1 md:grid-cols-2 gap-5">
              <table class="border-collapse border border-slate-400 w-full">
                <tbody>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Amount Placement
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Rp. {{ numberFormat(deposit.amount) }}
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Cashback
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      {{ item.rate }}%
                    </td>
                  </tr>
                  <tr>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Amount of Cashback
                    </td>
                    <td
                      class="border w-1/2 border-slate-300 py-2 px-4 text-left"
                    >
                      Rp. {{ numberFormat(item.amount || 0) }}
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </div>
        </div>

        <div class="w-full mb-8">
          <h2 class="font-medium text-lg pb-2">Note</h2>
          <div class="pt-4 grid grid-cols-1 md:grid-cols-2 gap-5">
            <textarea
              id="note"
              cols="30"
              rows="5"
              class="form-control resize-none"
              v-model.trim="deposit.note"
              :disabled="true"
              name="note"
            ></textarea>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { useDepositsStore } from "@/stores/deposit";
import { onMounted, computed, ref, watch } from "vue";
import { useRoute, useRouter } from "vue-router";
import { useNavStore } from "@/stores/nav";
import { depositNav, investmentNav } from "@/router/investment";
import { storeToRefs } from "pinia";
import { format } from "date-fns";
import { useModalStore } from "@/stores/modal";
import numeral from "numeral";
import { toast } from "vue3-toastify";

const route = useRoute();
const router = useRouter();
const depositStore = useDepositsStore();
const navStore = useNavStore();
const modalStore = useModalStore();

const id = route.params.id;

navStore.create([
  investmentNav.investment,
  depositNav.home,
  depositNav.viewPlacement,
]);

const { deposit } = storeToRefs(depositStore);

const isDelete = ref(false);
const dialogDelete = ref(false);
const modalDelete = ref(false);

const onClickEdit = () => {
  router.push({
    name: depositNav.editPlacement.name,
    params: { id: id },
  });
};

const findDeposit = async () => {
  if (id) {
    await depositStore.find(id as string);
  }
};

const numberFormat = (value: number) => {
  return numeral(value).format("0,0.[00]");
};

const onClickDelete = () => {
  modalStore.setModalDelete(true);
};

const onClickConfirmDelete = () => {
  // modalConfirmPassword.value = true;
  isDelete.value = true;
  modalStore.setModalDeleteReason(true);
};

const onConfirmPassword = async () => {
  const { error } = await depositStore.delete(
    String(deposit.value._id),
    modalStore.modalPasswordValue as string,
    modalStore.deleteReason
  );
  if (!error) {
    modalDelete.value = false;
    dialogDelete.value = false;
    modalStore.setModalDeleteReason(false);
    modalStore.setModalDelete(false);

    modalStore.setModalAlertSuccess(
      true,
      "Changes Saved!",
      "The selected data has been deleted."
    );
    // resetForm();
  } else {
    toast.error("Invalid password");
  }
};

const modalSuccessState = computed(() => modalStore.modalAlertSuccess);
const modalPasswordValueState = computed(() => modalStore.modalPasswordValue);
const confirmDeleteState = computed(() => modalStore.confirmDelete);
const confirmReqDeleteState = computed(() => modalStore.confirmRequestDelete);
watch(
  [
    modalSuccessState,
    modalPasswordValueState,
    confirmDeleteState,
    confirmReqDeleteState,
  ],
  async (
    [modalSuccess, modalPassword, confirmDelete, confirmReqDelete],
    [oldModalSuccess]
  ) => {
    if (
      !modalSuccess &&
      modalSuccess !== oldModalSuccess &&
      isDelete.value == true
    ) {
      router.push({ name: depositNav.placement.name });
    }

    if (modalPassword) {
      await onConfirmPassword();
    }

    if (confirmDelete) {
      onClickConfirmDelete();
      modalStore.setConfirmDelete(false);
    }
  }
);

onMounted(async () => {
  await findDeposit();
});
</script>
