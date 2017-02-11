# jp_code_english
The data contains all Japanese post codes in both English and Japanese

The data source in this github repository contains all japanese postal codes and their english and japanese addresses. 

If you are writing in Zoho Creator, here's the function that gets the postal code and returns english and japanese addresses as map. 

``` Javascript

map postal.get_address(string first_three, string second_four)
{
    this_address = map();
    first_three_len = ifnull(input.first_three,"").length();
    second_four_len = ifnull(input.second_four,"").length();
    if ((first_three_len  ==  3)  &&  (second_four_len  ==  4))
    {
        postal_code = input.first_three + input.second_four;
        data_url = "https://raw.githubusercontent.com/aorborc/jp_code_english/0804e74d63ec902eccfcf847ea49a0a6a7488d16/data/" + input.first_three + ".js";
        str = getUrl(data_url);
        value_map = str.toMap();
        my_map = (value_map.get(postal_code)).toMap();
        jp_address = ((my_map.get("perfecture_jp")) + my_map.get("jp_add_1")) + my_map.get("jp_add_2");
        eng_address = ((my_map.get("prefecture")) +" " +  my_map.get("city")) + " " +  my_map.get("town");
        this_address.put("jp_address", jp_address);
        this_address.put("eng_address", eng_address);
    }
    return this_address;
}

```
