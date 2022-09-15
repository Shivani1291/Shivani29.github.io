# Shivani29.github.io
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://cdn.tailwindcss.com"></script>
    <title>Survey Form</title>
</head>

<body>
    <div class="relative flex min-h-screen flex-col justify-center overflow-hidden py-6 bg-gray-50">
        <div
            class="relative bg-white px-6 pt-5 pb-5 shadow-xl ring-1 ring-gray-900/5 sm:mx-auto sm:max-w-lg sm:rounded-lg sm:px-10">
            <div class="mx-auto max-w-md">
                <h2 class="text-3xl text-center font-bold leading-tight">
                    Survey Form
                </h2>
                <div class="divide-y divide-gray-300/50">
                    <div class="space-y-6 py-8 text-base leading-7 text-gray-600">
                        <form id="user_form">
                            <label for="name" class="text-md w-40 inline-block font-medium leading-5 text-gray-700">
                                Name
                            </label>
                            <input required type="text" id="name" name="name" class="bg-gray-100 inline-block rounded-lg shadow-md px-4 py-3 mb-5 text-base leading-6 placeholder-gray-500 focus:outline-none focus:placeholder-gray-400 transition duration-150 ease-in-out invalid:border-pink-500 invalid:text-pink-600
                            focus:invalid:border-pink-500 focus:invalid:ring-pink-500"
                                placeholder="Enter full name"></br>

                            <label for="email" class="text-md w-40 inline-block font-medium leading-5 text-gray-700">
                                Email
                            </label>
                            <input required type="email" id="email" name="email" class="bg-gray-100 inline-block rounded-lg shadow-md px-4 py-3 mb-5 text-base leading-6 placeholder-gray-500 focus:outline-none focus:placeholder-gray-400 transition duration-150 ease-in-out invalid:border-pink-500 invalid:text-pink-600
                            focus:invalid:border-pink-500 focus:invalid:ring-pink-500" placeholder="Enter email"></br>

                            <label for="password" class="text-md w-40 inline-block font-medium leading-5 text-gray-700">
                                Password
                            </label>
                            <input required type="password" id="password" name="password" class="bg-gray-100 inline-block rounded-lg shadow-md px-4 py-3 mb-5 text-base leading-6 placeholder-gray-500 focus:outline-none focus:placeholder-gray-400 transition duration-150 ease-in-out invalid:border-pink-500 invalid:text-pink-600
                            focus:invalid:border-pink-500 focus:invalid:ring-pink-500"
                                placeholder="Enter password"></br>

                            <label for="dob" class="text-md w-40 inline-block font-medium leading-5 text-gray-700">
                                Date of Birth
                            </label>
                            <input required type="date" id="dob" name="dob" class="bg-gray-100 inline-block rounded-lg shadow-md px-4 py-3 mb-5 text-base leading-6 placeholder-gray-500 focus:outline-none focus:placeholder-gray-400 transition duration-150 ease-in-out invalid:border-pink-500 invalid:text-pink-600
                            focus:invalid:border-pink-500 focus:invalid:ring-pink-500"></br>

                            <label for="acceptTerms"
                                class="text-md w-50 inline-block font-medium leading-5 text-gray-700">
                                Accept Terms & Conditions
                            </label>
                            <input required type="checkbox" id="acceptTerms" name="acceptTerms"
                                class="bg-gray-100 inline-block rounded-lg shadow-md px-4 py-3 mb-5 text-base leading-6 placeholder-gray-500 focus:outline-none focus:placeholder-gray-400 transition duration-150 ease-in-out"></br>

                            <button type="submit"
                                class="w-fit rounded-lg shadow-lg px-8 py-4 bg-green-500 text-white hover:bg-green-400 focus:outline-none focus:shadow-outline transition duration-150 ease-in-out">
                                Submit
                            </button>
                        </form>
                    </div>
                </div>
            </div>
        </div>

        <div
            class="relative bg-white px-6 mt-5 pt-10 pb-8 shadow-xl ring-1 ring-gray-900/5 sm:mx-auto sm:rounded-lg sm:px-10">
            <div class="mx-auto">
                <h2 class="text-3xl text-center font-bold leading-tight">
                    Entries
                </h2>
                <div class="divide-y divide-gray-300/50" id="user-entries">
                </div>
            </div>
        </div>
    </div>

    <script>

        let today = new Date();
        let dd = today.getDate();
        let mm = today.getMonth() + 1; //January is 0 so need to add 1 to make it 1!
        let yyyy = today.getFullYear();
        if (dd < 10) {
            dd = '0' + dd
        }
        if (mm < 10) {
            mm = '0' + mm
        }
        maxDate = yyyy - 18 + '-' + mm + '-' + dd;
        minDate = yyyy - 55 + '-' + mm + '-' + dd;
        document.getElementById("dob").setAttribute("min", minDate);
        document.getElementById("dob").setAttribute("max", maxDate);

        let userEntries = localStorage.getItem("user-entries");
        if (userEntries) {
            userEntries = JSON.parse(userEntries);
        } else {
            userEntries = [];
        }

        const displayEntries = () => {
            const savedUserEntries = localStorage.getItem("user-entries");
            let entries = "";
            if (savedUserEntries) {
                const parsedUserEntries = JSON.parse(savedUserEntries);
                entries = parsedUserEntries
                    .map((entry) => {
                        const name = `<td class='border px-4 py-2'>${entry.name}</td>`;
                        const email = `<td class='border px-4 py-2'>${entry.email}</td>`;
                        const password = `<td class='border px-4 py-2'>${entry.password}</td>`;
                        const dob = `<td class='border px-4 py-2'>${entry.dob}</td>`;
                        const acceptTerms = `<td class='border px-4 py-2'>${entry.acceptTermsAndConditions}</td>`;
                        const row = `<tr>${name} ${email} ${password} ${dob} ${acceptTerms}</tr>`;
                        return row;
                    })
                    .join("\n");
            }
            var table = `<table class="table-auto w-full"><tr>
          <th class="px-4 py-2">Name</th>
          <th class="px-4 py-2">Email</th>
          <th class="px-4 py-2">Password</th>
          <th class="px-4 py-2">Dob</th>
          <th class="px-4 py-2">Accepted terms?</th>
        </tr>${entries} </table>`;
            let details = document.getElementById("user-entries");
            details.innerHTML = table;
        };

        const saveUserForm = (event) => {
            event.preventDefault();
            event.preventDefault();
            const name = document.getElementById("name").value;
            const email = document.getElementById("email").value;
            const password = document.getElementById("password").value;
            const dob = document.getElementById("dob").value;
            const acceptTermsAndConditions =
                document.getElementById("acceptTerms").checked;
            const userDetails = {
                name,
                email,
                password,
                dob,
                acceptTermsAndConditions,
            };
            userEntries.push(userDetails);
            localStorage.setItem("user-entries", JSON.stringify(userEntries));

            displayEntries(); // Add this line
        };

        let form = document.getElementById("user_form");
        form.addEventListener("submit", saveUserForm, true);
        displayEntries();

    </script>

</body>
</html>
