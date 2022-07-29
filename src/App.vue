<template>
  <main class="bg-gray-100 min-h-screen px-3 min-w-screen">
    <main class="container mx-auto">
      <main class="flex flex-col justify-center items-center h-screen">
        <h1 class="text-3xl font-bold text-black/90 py-5">
          Credit Card Number Validator
        </h1>
        <div class="w-full lg:max-w-160">
          <form @submit.prevent="checker" class="">
            <div class="relative">
              <div
                class="flex absolute inset-y-0 left-0 items-center pl-3 pointer-events-none"
              >
                <svg
                  class="w-5 h-5 text-gray-500 dark:text-gray-400"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"
                  ></path>
                </svg>
              </div>
              <input
                type="text"
                v-maska="'#### #### #### ####'"
                v-model="cardNumber"
                class="block p-4 pl-10 lg:min-w-160 w-full text-sm text-gray-900 outline-none bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
                placeholder="Credit Card Number"
                required
              />
              <button
                type="submit"
                class="text-white absolute right-2.5 bottom-2.5 focus:ring-blue-300 font-medium rounded-lg text-sm px-4 py-2 bg-gradient-22 outline-none"
              >
                Check
              </button>
            </div>
            <p
              :class="[error ? 'text-red-500' : 'text-green-500']"
              class="text-xs"
            >
              &nbsp;{{ error }}
            </p>
          </form>
        </div>
      </main>
    </main>
  </main>
  <main>
    <div class="fixed bottom-0 right-0">
      <button class="py-5 px-8 bg-black/90 rounded-tl-xl">
        <a
          class="text-white"
          target="_blank"
          href="https://www.github.com/atif0075"
        >
          <svg
            fill="currentColor"
            viewBox="0 0 16 16"
            xmlns="http://www.w3.org/2000/svg"
            class="w-5 h-5"
          >
            <path
              d="M7.975 16a9.39 9.39 0 003.169-.509c-.473.076-.652-.229-.652-.486l.004-.572c.003-.521.01-1.3.01-2.197 0-.944-.316-1.549-.68-1.863 2.24-.252 4.594-1.108 4.594-4.973 0-1.108-.39-2.002-1.032-2.707.1-.251.453-1.284-.1-2.668 0 0-.844-.277-2.77 1.032A9.345 9.345 0 008 .717c-.856 0-1.712.113-2.518.34C3.556-.24 2.712.025 2.712.025c-.553 1.384-.2 2.417-.1 2.668-.642.705-1.033 1.612-1.033 2.707 0 3.852 2.342 4.72 4.583 4.973-.29.252-.554.692-.642 1.347-.58.264-2.027.692-2.933-.831-.19-.302-.756-1.045-1.549-1.032-.843.012-.34.478.013.667.428.239.919 1.133 1.032 1.422.201.567.856 1.65 3.386 1.184 0 .55.006 1.079.01 1.447l.003.428c0 .265-.189.567-.692.479 1.007.34 1.926.516 3.185.516z"
            ></path>
          </svg>
        </a>
      </button>
    </div>
  </main>
</template>
<script setup>
import { ref } from "vue";
let error = ref("");
let cardNumber = ref("");
let cardNumberDigits = ref([]);
let checker = () => {
  // split card number into array of digits
  cardNumberDigits.value = cardNumber.value.split("");
  //   remove spaces from array
  cardNumberDigits.value = cardNumberDigits.value.filter(
    (digit) => digit !== " "
  );
  //   double every second digit and add to array
  cardNumberDigits.value = cardNumberDigits.value.map((digit, index) => {
    if (index % 2 === 0) {
      return digit * 2;
    } else {
      return digit;
    }
  });
  //   convert array of digits to string
  cardNumberDigits.value = cardNumberDigits.value.join("");
  //   convert string to array of digits
  cardNumberDigits.value = cardNumberDigits.value.split("");
  console.log(cardNumberDigits.value);
  //   sum all digits
  let sum = 0;
  let lastDigit = parseInt(cardNumberDigits.value.pop());
  cardNumberDigits.value.forEach((digit) => {
    sum += parseInt(digit);
  });
  sum = sum / 10;
  sum = sum.toString();
  sum = sum.split("");
  sum = parseInt(sum.pop());
  let result = 10 - sum;
  if (result === lastDigit) {
    error.value = "This card is valid";
  } else {
    error.value = "This card is invalid";
  }

  console.log(sum);
};
</script>
<style></style>
