polygon migratin tool notes

login - uses email not usernam bcuz custom user model. only staff user can acsess it. if is_staff false it wont let u login even if pw is corect

fetch problem - enter polygon id and click fetch. it uses sha512 signing to pull prob details, statment, tests and solutins from polygon api. nothng is saved to db yet just stays in sessoin

migrate to db - select dificulty and min 2 tags. existing problm get upated using polygon_id. tags are manytomany

test cases - regular tests save in ProblemTestCase and smaple tests go in SampleTestCase too. but input and output get cut to 260 charecters so db dont have full test case data

azure upload - AzureTestcase.py uploads files to test_cases/problemid/ and answe files use .a extention

env stuff - both polygon api key and secret must be in .env or app wont even start throws eror in settings.py line 127
