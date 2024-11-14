# READING ALL COOKIES

# Create view in views.py

def Cookies(req):
    cookies = req.COOKIES
    return render(req,'PayRollApp/Cookies.html',{'cookies':cookies})

# Create Cookies.html(Reading all cookies)

{% for key, value in cookies.items %}
    <tr>
        <td>{{ key }}</td>
        <td>{{ value }}</td>
    </tr>
{% endfor %}



# CREATING COOKIES

* create new view

def add_cookie(req):
    if req.method == 'POST':
        cookie_name = req.POST.get('cookie_name')
        cookie_value = req.POST.get('cookie_value')
        response = HttpResponseRedirect(reverse('Cookies'))
        response.set_cookie(cookie_name,cookie_value,120)   // here we can add esxpire time then it will removed from cookie storage
        return response
    return JsonResponse({'message':'Invalid Request'})

* in html

<form action="{% url 'add_cookie' %}" method="post" id="addCookieForm">
     {% csrf_token %}
     <div class="form-group">
         <label for="cookie_name">Cookie Name: </label>
         <input type="text" class="form-contrname="cookie_name" required>
                    </div>
      <div class="form-group">
          <label for="cookie_value">Cookie Value: </label>
          <input type="text" class="form-controbtn-secondary">Add Cookie</button>
</form>

# Deleting COokies

* create view

def clear_cookies(req):
    response = HttpResponseRedirect(reverse('Cookies'))
    for key in req.COOKIES:
        response.delete_cookie(key)
    return response


* in html 

 <a href="{% url 'clear_cookies' %}" class="btn btn-primary">delete  all cookie</a>
 