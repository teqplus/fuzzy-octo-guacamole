# fuzzy-octo-guacamole
Learn Project
// All valid credit card numbers
const valid1 = [4, 5, 3, 9, 6, 7, 7, 9, 0, 8, 0, 1, 6, 8, 0, 8];
const valid2 = [5, 5, 3, 5, 7, 6, 6, 7, 6, 8, 7, 5, 1, 4, 3, 9];
const valid3 = [3, 7, 1, 6, 1, 2, 0, 1, 9, 9, 8, 5, 2, 3, 6];
const valid4 = [6, 0, 1, 1, 1, 4, 4, 3, 4, 0, 6, 8, 2, 9, 0, 5];
const valid5 = [4, 5, 3, 9, 4, 0, 4, 9, 6, 7, 8, 6, 9, 6, 6, 6];

// All invalid credit card numbers
const invalid1 = [4, 5, 3, 2, 7, 7, 8, 7, 7, 1, 0, 9, 1, 7, 9, 5];
const invalid2 = [5, 7, 9, 5, 5, 9, 3, 3, 9, 2, 1, 3, 4, 6, 4, 3];
const invalid3 = [3, 7, 5, 7, 9, 6, 0, 8, 4, 4, 5, 9, 9, 1, 4];
const invalid4 = [6, 0, 1, 1, 1, 2, 7, 9, 6, 1, 7, 7, 7, 9, 3, 5];
const invalid5 = [5, 3, 8, 2, 0, 1, 9, 7, 7, 2, 8, 8, 3, 8, 5, 4];

// Can be either valid or invalid
const mystery1 = [3, 4, 4, 8, 0, 1, 9, 6, 8, 3, 0, 5, 4, 1, 4];
const mystery2 = [5, 4, 6, 6, 1, 0, 0, 8, 6, 1, 6, 2, 0, 2, 3, 9];
const mystery3 = [6, 0, 1, 1, 3, 7, 7, 0, 2, 0, 9, 6, 2, 6, 5, 6, 2, 0, 3];
const mystery4 = [4, 9, 2, 9, 8, 7, 7, 1, 6, 9, 2, 1, 7, 0, 9, 3];
const mystery5 = [4, 9, 1, 3, 5, 4, 0, 4, 6, 3, 0, 7, 2, 5, 2, 3];

// An array of all the arrays above
const batch = [valid1, valid2, valid3, valid4, valid5, invalid1, invalid2, invalid3, invalid4, invalid5, mystery1, mystery2, mystery3, mystery4, mystery5];


// Add your functions below:
// validateCred function to validate correct Credit Cards
const validateCred = array => {
  let odd = [];
  let even = [];
  let sumOdd = 0;
  let sumEven = 0;
  for (let i = array.length - 1; i >= 0; i-=2) {
    odd.push(array[i]);
    sumOdd += array[i];
  }
  for (let j = array.length - 2; j >= 0; j-=2) {
    let sum2 = array[j] * 2;
    let sum3 = 0;
    if (sum2 > 9){
      sum3 = sum2 - 9;
      sumEven += sum3;
      even.push(sum3);
    } else{
      sumEven += sum2
      even.push(sum2);
    }
  }
 let sumOfCredit = 0;
  sumOfCredit = sumEven + sumOdd;

  if (sumOfCredit % 10 === 0) {
        return true;
    }
    else {
        return false;
    }

    };
// End of validateCred function to validate correct Credit Cards

// invalidCards function to find  invalid Credit Cards and store that information

let invalidCards = [];
const findInvalidCards = nestedArray => {
  for (let i = nestedArray.length - 1; i >= 0; i--){
    validateCred(nestedArray[i]);
    if(validateCred(nestedArray[i]) === false){
            invalidCards.push(nestedArray[i]);   
      }
  } 
} 
// End of invalidCards function
findInvalidCards(batch);



// idInvalidCardCompanies function to identify which credit card company
var arrayOfCompaniesSorted = [];
const idInvalidCardCompanies = anotherNestedArray => {
    var lengthOfCards = invalidCards.length;
    var i = lengthOfCards-1;
    
  
    // arrays to hold each companies invalid cards (if any)
    // amex starts 3
    var amex = [];
    // visa starts 4
    var visa = [];
    // mastercard starts 5
    var mastercard = [];
    // discover starts 6
    var discover = [];

    do {
        switch(invalidCards[i][0]){
            case(3):
            amex.push(invalidCards[i])
            break;

            case(4):
            visa.push(invalidCards[i])
            break;

            case(5):
            mastercard.push(invalidCards[i])
            break;

            case(6):
            discover.push(invalidCards[i])
            break;
        }
        i--;          
    } while (i >= 0);
     
     
     
     // return the card companies in one nested array
    if (visa.length > 0){
      arrayOfCompaniesSorted.push('Visa');
    } 
    if (amex.length > 0){
      arrayOfCompaniesSorted.push('Amex');
    } 
    if (mastercard.length > 0){
      arrayOfCompaniesSorted.push('Mastercard');
    } 
    if (discover.length > 0){
      arrayOfCompaniesSorted.push('Discover');
    } 
    
    
    console.log(arrayOfCompaniesSorted);
    
}
// end of InvalidCardCompanies function

idInvalidCardCompanies(invalidCards);
