
graph = {
    'Germany': ['Poland', 'Czech Republic', 'Austria', 'Switzerland'],
    'Poland': ['Germany', 'Czech Republic', 'Slovakia'],
    'Slovakia': ['Poland', 'Czech Republic', 'Hungary'],
    'Switzerland': ['Germany', 'Austria', 'Italy'],
    'Austria': ['Germany', 'Switzerland', 'Czech Republic',
                'Hungary', 'Italy', 'Slovenia'],
    'Czech Republic': ['Germany', 'Poland', 'Slovakia', 'Austria'],
    'Hungary': ['Slovakia', 'Austria', 'Slovenia'],
    'Slovenia': ['Hungary', 'Italy', 'Austria'],
    'Italy': ['Switzerland', 'Austria', 'Slovenia']
}

colors = ['Red', 'Green', 'Blue', 'Yellow']
result = {}

def safe(country, color):
    for neighbor in graph[country]:
        if result.get(neighbor) == color:
            return False
    return True

def color_map(countries):
    if not countries:
        return True

    country = countries[0]

    for color in colors:
        if safe(country, color):
            result[country] = color

            if color_map(countries[1:]):
                return True

            del result[country]

    return False

if color_map(list(graph)):
    for country in graph:
        print(country, ":", result[country])
else:
    print("No solution")
