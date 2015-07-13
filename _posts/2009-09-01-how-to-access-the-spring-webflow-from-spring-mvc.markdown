---
layout: post
title: How to access the Spring WebFlow from Spring MVC
tags:
- Java
---

I recently came across a problem in a [Spring
Webflow](http://www.springsource.org/webflow) based application where I
needed to have one page as a standard [Spring
MVC](http://static.springsource.org/spring/docs/2.0.x/reference/mvc.html)
page. I needed to write a PDF file to the actual http response and I'm
not allowed to do that in WebFlow. So I defined a standard Spring [MVC
Controller](http://static.springsource.org/spring/docs/2.0.x/reference/mvc.html#mvc-controller)
and [URL
Mapper](http://static.springsource.org/spring/docs/2.0.x/api/org/springframework/web/servlet/handler/SimpleUrlHandlerMapping.html)
to complement my existing [Flow
Controller](http://static.springsource.org/spring-webflow/docs/1.0.5/api/org/springframework/webflow/executor/mvc/FlowController.html):

    <bean id="urlMapping" class="org.springframework.web.servlet.handler.SimpleUrlHandlerMapping">
      <property name="mappings">
        <props>
          <prop key="/index.htm">/index.htm</prop>
          <prop key="/pdf.htm">PDFPageController</prop>
        </props>
      </property>
    </bean>


    <bean id="PDFPageController" class="controller.mvc.PDFPageController" />


    <bean name="/index.htm" class="org.springframework.webflow.executor.mvc.FlowController">
    <property name="flowExecutor" ref="flowExecutor" />
    <property name="defaultFlowId" value="main" />
    </bean>

Then inside the MVC Controller (which extends
[AbstractController](http://static.springsource.org/spring/docs/2.5.x/api/org/springframework/web/servlet/mvc/AbstractController.html)),
define a method called accessFlowScope like below:

    private void accessFlowScope(HttpServletRequest request, HttpServletResponse response) {
      // Gain access to the Spring Web Flow context
      FlowController controller = (FlowController)getApplicationContext().getBean("/pdf.htm");
      FlowExecutionRepository repository = ((FlowExecutorImpl)controller.getFlowExecutor()).getExecutionRepository();
      FlowExecutorArgumentHandler handler = controller.getArgumentHandler();
      ExternalContext externalContext = new ServletExternalContext(getServletContext(), request, response);

      // Make sure we have a flow execution key.
      if (handler.isFlowExecutionKeyPresent(externalContext)) {
        try {
          // Get access to the variable stored in the context.
          ExternalContextHolder.setExternalContext(externalContext);
          FlowExecutionKey flowExecutionKey = repository.parseFlowExecutionKey(handler.extractFlowExecutionKey(externalContext));
          FlowExecution flowExecution = repository.getFlowExecution(flowExecutionKey);
          Object variableInFlowScopeObject = flowExecution.getActiveSession().getScope().get("variableInFlowScope");
        }
        catch(Exception ex) {
          logger.error("Error when accessing flow scope from MVC", ex);
        }
        finally {
          ExternalContextHolder.setExternalContext(null);
        }

      }
      else {
        logger.error("Handler did not have flow execution key present");
      }
    }

This can then be called from your
[handleRequestInternal](http://static.springsource.org/spring/docs/1.2.x/api/org/springframework/web/servlet/mvc/AbstractController.html#handleRequestInternal%28javax.servlet.http.HttpServletRequest,%20javax.servlet.http.HttpServletResponse%29)
method of the MVC controller:

    public ModelAndView handleRequestInternal(HttpServletRequest request, HttpServletResponse response)

All that is required now is to call from the Webflow view jsp into the
MVC controller. I had to do a horrible iframe like so:

    <iframe id="pdf-view" src="pdf.htm?_flowExecutionKey=${flowExecutionKey}" height="100%" width="50%">
      I'm sorry, iframes are not supported by your browser, upgrade to <a href="http://getfirefox.com">Firefox</a>
    </iframe>

Now you can pull out whatever values you require from the many scopes
(request, flash, flow, conversation) and use them in your MVC controller
to do stuff. NB: All the code is used pretty much verbatim from
http://www.ervacon.com/products/swf/tips/tip1.html, but it doesn't say
to add the flowExecutionKey onto the URL, which is the part I was
missing and thiking that it wasn't working correctly.
